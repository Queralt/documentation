Platform Documentation
=============
 * [Data Vectors](Data Vectors.md)

After signing up, you will be given an API key by Queralt.

All calls use the API key sent in the `X-API-KEY` header. Calls are versioned at the root level of the URL. For example, to list all data vectors, an API client would send:

     GET http://{api_base}/0.2/dataVectors/


## Error Handlng

If a call returns an HTTP status code of `200`, it will return the results expected in the documentation

| Code | Description |
| ------------- | ------------- |
| 200      | The response will be as expected |
| 400      | The input parameters are invalid |
| 401      | API key is invalid |
| 404      | Not found, The path is invalid |
| 500      | Internal error |

If a status code other than `200` or `404` is returned, the body of the response will contain an error with additional details about the issue, in the following format:
```json
{
     "error": {
          "code": "D01",
          "message": "Something did not go as planned"
     }
}
```
