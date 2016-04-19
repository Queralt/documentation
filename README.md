Platform Documentation
=============

When a developer signs up, they are assigned an API key and a secret by Queralt.

All calls use the API key sent in the `x-api-key` header. Calls are versioned at the root level of the URL. For example, to list all data vectors, an API client would send:

     GET https://{api_base}/0.2/dataVectors/
     
## Request Signing

All calls to the platform must be signed with the developer's secret. For more information, see [Request Signatures](Request Signing.md).

## Error Handlng

If a call returns an HTTP status code of `200`, it will return the results expected in the documentation

| Code | Description |
| ------------- | ------------- |
| 200      | The response will be as expected |
| 400      | The input parameters are invalid |
| 401      | Authentication failed, API key or request improperly signed |
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

## API calls
There are four major categories of API calls, `data vectors`, `actuators`, `actions`, and `subscription`.
 * [Data Vectors](Data Vectors.md)
 * [Actuators](Actuators.md)
 * [Actions](Actions.md)
 * [Subscription](Subscription.md)
