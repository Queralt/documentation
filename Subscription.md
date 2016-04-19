Subscription
=============

The subscription API contains one single call.

### GET /subscription/
Return usage details about the platform usage for a given API key. There are no parameters.
```
GET /subscription/
```
Return:
```json
{
    "dataVectors": {
        "count": 562,
        "events": {
            "count": 89371
        }
    },
    "actuators": {
        "count": 1,
        "actions": {
            "count": 24
        }
    },
    "modules": {
        "count": 5
    },
}
```