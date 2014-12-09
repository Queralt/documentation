Sessions
=============

The session API calls are used to create or validate session keys. Session keys are then used in conjunction with API key signatures to authenticate all calls made to the platform.


## /session/create/

Used by API clients to create a session key using their API key and signature. The resulting session key is an alphanumeric string of indeterminate length.

Input Variables

   * API Key - Given to API client by Queralt on account creation
   * Signature - Given to API client by Queralt on account creation
   * Instance - The ID of the instance the API client is attempting to create a session for

Input
```json
{
    "data": {
        "apiKey": "xxx", 
        "signature": "yyy", 
        "instance": "zzz"
    }
}
```

Return
```json
{
    "data": {
        "session": {
            "key": "8a6be800b5a24718707aa98", 
            "expiration": {
                "date": 1381349923, 
                "validFor": 1997693
            }
        }
    }, 
    "status": {
        "description": "Everything went as planned.", 
        "success": true, 
        "time": 1379352230
    }
}
```

## /session/validate/

Ensure that a specified session key is still valid

Input Variables

   * Session - Retrieved from the /session/create/ API call
   * Signature - Given to API client by Queralt

Input
```json
{
    "data": {
        "session": "xxx", 
        "signature": "yyy"
    }
}
```

Return
```json
{
    "session": {
        "valid": true, 
        "session": "xyz", 
        "expiration": {
            "expires": 1381349923, 
            "validFor": 1997693
        }
    }, 
    "status": {
        "description": "Everything went as planned.", 
        "success": true, 
        "time": 1379352230
    }
}
```
