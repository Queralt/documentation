Actions
=============

The actions API is used by actuators to request actions to execute.

## /actions/open/

Called by an actuator to recieve a list of actions that have yet to be dismissed.

Input Variables

   * ID - The identifier of the actuator to request actions for.
   * Connectors - Key value pair used to refer to the actuator. Required, if ID is omitted.

Input
```json
{
    "authentication": { }, 
    "data": {
        "connector": {
            "id": "C02G2680DRHF", 
            "type": "door"
        }
    }
}
```

Return
```json
{
    "status": {
        "success": true, 
        "time": 1414197936.2658, 
        "description": "Everything went as planned."
    }, 
    "data": {
        "actions": [
            {
                "id": "1", 
                "time": 1410197636, 
                "type": "open", 
                "data": {
                    "parameter": true
                }
            }
        ]
    }
}
```

## /actions/dismiss/

When an actuator has executed an action, this call is used to mark that action as 'dismissed'.

Input Variables

   * ID - The identifier of the action which has been executed

Input
```json
{
   "authentication": { },
   "data": {
      "id": 1
   }
}
```

Return
```json
{
    "status": {
        "success": true, 
        "time": 1414197936.2658, 
        "description": "Everything went as planned."
    }
}
```
