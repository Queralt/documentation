Request Signatures
=============

In all API requests, the HTTP method, path, query string, headers and body are signed with a secret and sent as the request's "signature." The headers include the user's API key, as well as a timestamp of when the request was made. On the server, the request is confirmed against the signature. If the signature does not match, the request is rejected. If the server receives a request with a timestamp older than five minutes, it is also rejected.

This enables three things:
- Verify the authenticity of the client
- Prevent MITM attack
- Protect against replay attacks

The client's authenticity is confirmed by their continued ability to produce signatures based on their secret. This approach also prevents man-in-the-middle attacks because any tampering would result in the signature mismatching the request's contents. Finally, replay attacks are prevented because signed requests with old timestamps will be rejected.

Each request requires three headers: `x-api-key`, `date`, and `authorization`. If the HTTP request contains a body, you must also send the `content-length` and `content-type` headers.

The `x-api-key` header should contain the string representation of the user's API key.

The `date` header is a standard [RFC-822 (updated in RFC-1123)](https://tools.ietf.org/html/rfc822#section-5) date, as per [RFC-7231](https://tools.ietf.org/html/rfc7231#section-7.1.1.2).

The `authorization` header is a standard as per [RFC-2617](https://tools.ietf.org/html/rfc2617#section-3.2.2) that, confusingly, is designed for authentication and not authorization. It contains a signature of the entire request.

To calculate the signature, you first need to create a string representation of the request. When the platform recieves an authenticated request, it computes the the signature and compares it with the signature you provided. Therefore, you must create a string representation of the request in the exact same way as the platform. This is called "canonicalization."

The format of a canonical representation of a request is:
```
     HTTP Verb + \n
     URI + \n
     Canonical query string + \n
     Canonically formatted signed headers + \n
     Hashed payload
```

The canonical representations of these elements are as follows

|Component|Format|Example|
|---------|------|-------|
|HTTP Verb | upperCase(verb) | POST, GET or DELETE |
|URI | encode(uri) | /0.2/dataVectors/test%20item|
|Query String | encode(paramA) + '=' + encode(valueA) + '&' + encode(paramB) + '=' + encode(valueB) | paramA=valueA&paramB=value%20B |
|Headers | lowerCase(keyA) + ':' + trim(valueA) + '\n' + lowerCase(keyB) + ':' + trim(valueB) | keyA:valueA<br>keyB:value%20B 
|Hashed payload | hex(hash('sha256', bodyData)) | ... |

The HTTP verb must be upper case. The URI should be url-encoded. The query string elements should be alphabetically sorted. The header keys must all be lower case (as per [RFC-2616](http://www.ietf.org/rfc/rfc2616.txt)) and alphabetically sorted. The only headers included in the signature should be: `x-api-key`, `date`, and optionally `content-length` and `content-type` if the HTTP body is not empty. The last line of the request string should be a hex representation of a SHA256 hash of the request body. If there is no request body, it should be the hash of an empty string.

Programatically:
```
     upperCase(method) + \n
     path + \n
     encode(paramA) + '=' + escape(valueA) + '&' + escape(paramB) + '=' + escape(valueB) + \n
     lowerCase('a-api-key') + ':' + trim(_API_KEY_) + \n + lowerCase(content-length) + ':' + trim('15') + \n
     hex(hash('sha256', bodyData)) + \n
```

For Example
```
     POST
     /0.2/dataVectors/test
     paramA=valueA&paraB=value%20B
     content-length:15
     date:Tue, 20 Apr 2016 18:48:24 GMT
     x-api-key:12345
     8eb2e35250a66c65d981393c74cead26a66c33c54c4d4a327c31d3e5f08b9e1b
```
     
Then, calculate the HMAC signature of the entire request by signing it with the user's secret, and get the hex representation:
```
let signature = hex(hmacSha256(secret, requestString))
```

Send that value as the contents of the `authorization` header, with the preceding value 'signature.'
```
headers[authorization] = 'signature ' + signature
```

If request validation fails, the platform will respond with HTTP code `401` and a JSON response containing information about the failure.
```json
{
     "error": {
          "message": "Missing timestamp. Please timestamp all incoming requests by including 'date' header."
     }
}
```
