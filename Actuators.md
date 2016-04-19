Actuators
=============

Actuators are logical entities that represent a device or construct that the platform will send commands to. They are modeled as documents. The primary usage of actuators is to recieve actions dictated by the platform, however they can also store some free-form information about themselves.


### GET /actuators/
List all existing actuators

```
GET /actuators/
```
Return:
```json
[
	{
        "id": "front_door_lock"
    },
    {
        "id": "back_door_lock"
    }
]
```


### GET /actuators/:identifier
Retrieve the full state of an actuator with the specified identifier.

```
GET /dataVectors/front_door_lock
```
Return:
```json
{
	"id": "front_door_lock",
	"brand": "Locksmith, LLC",
    "serial number": "6191237HSH31"
}
```


### POST /actuators/:identifier
Update an actuator with the specified identifier. If one does not yet exist, it will be created with the specified data.
```
POST /dataVectors/front_door_lock
```
```json
{
	"color": "golden"
}
```
There is no return data for this call.


### POST /actuators/
Create a new actuator, with all attributes specified in the body. An identifier will be returned to the user.
```
POST /dataVectors/
```
```json
{
	"style": "key"
}
```
Return
```json
{
	"id": "vsdjsdfj124123fefg56"
}
```


### DELETE /actuators/:identifier

Delete an actuator with the specified identifier. If no actuator with that identifier is found, return an error. Otherwise, return nothing.
```
DELETE /dataVectors/front_door_lock
```
There is no return data for this call.



# Actions

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
Marks an existing action as "completed", while appending a small amount of information into the action itself. This is designed so that an actuator can add information about the execution of the action for later viewing. For example, the actuator could add the name of the person who dismissed an alert to the alert itself.

```
POST /actuators/front_door_lock/actions/12h1h23
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


# Push Actuators

By default, actuators must request a list of actions sent to them using the [actions API](Actions.md). However, they may also register themselves as "remote" actuators that can recieve commands directly. To do this, set an attribute on an actuator called "location" with the host, port and path it will recieve messages on. 
```
POST /dataVectors/front_door_lock
```
```json
{
	"location": {
        "host": "testingactuators.com",
        "port": 2112,
        "path": "/actuator"
    }
}
```

Once registered, all actions will be sent to the actuator as HTTP requests in the following format:
```json
{
    "id": "2436gg13",
    "time": 1436742773,
    "data": {
        "description": "The \"data\" node contains freeform information as specified by rules registered in the platform",
        "type": "door_open"
    }
}
```