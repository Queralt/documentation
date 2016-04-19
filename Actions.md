Actions
=============

Actions are commands sent from the platform to [actuators](Actuators.md). An actuator can either periodically request commands to be executed, or register itself as a "push" actuator and recieve actions directly.

### GET /actuators/:identifier/actions/
Retrieves a list of actions created for a specified actuator. Actions contain an identifier, timestamp, a "completed" status boolean that represents whether or not an action has been executed, and a freeform "data" node that contains whatever information the actuator needs to perform the task.

```
GET /actuators/front_door_lock/actions/
```
Return:
```json
[
    {
    	"id": "12h1h23",
    	"time": 14112331242,
    	"completed": false,
    	"data": {
        	"type": "unlock"
        }
    },
    {
    	"id": "71nwj4",
    	"time": 14112331000,
    	"completed": true,
    	"data": {
        	"type": "lock"
    	}
    }
]
```

### DELETE /actuators/:actuator/actions/:action
Marks an existing action as "completed"

```
DELETE /actuators/front_door_lock/actions/12h1h23
```
There is no return for this call.


### POST /actuators/:actuator/actions/:action
Marks an existing action as "completed", while appending a small amount of information into the 

```
DELETE /actuators/front_door_lock/actions/12h1h23
```
POST
```json
{
    "informationAboutTheExecutionOfAnAction": {
        "howLongDoorLockTook": 5.012
    }
}
```

There is no return for this call.
