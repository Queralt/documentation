Platform Documentation
=============
 * [Sessions](Session.md)
 * [Data Vectors](Data Vectors.md)
 * [Actions](Actions.md)

When a developer signs up, they are assigned an API key and a secret by Queralt. They can then create an instance to begin working in.

To begin working in an instance of the platform, you must create a session. Sessions are created using the /session/create/ call. It accepts three parameters: the instance key, the API key, and signature. The instance key is returned to the developer after creating an instance, and the signature is a SHA512 hash containing the instance, API key, and secret.

All other API calls use the session key, in conjunction with the same signature from the session creation call for authentication. Calls are versioned at the root level. So, to make the 'data vectors list' API call, the POST data destination would be:
     http://{api_base}/0.1/dataVectors/list/

To make a request to this call, the POST data would be:
```json
{ 
     "authentication": {
           "session": "foo", 
          "signature": "bar"
     },
     "data": {
        "attributes": [
          "temperature"
        ]
     }
}
```

All information returned is contained in the “data” node of the response JSON. In addition (and as per the documentation) all input variables are also contained within a "data" node of the input JSON.
