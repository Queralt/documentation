Data Vector Query Operators 
=============

The `GET /dataVectors/` API is used for retrieving all information from the platform. It's `criteria` parameter enables afiltering by all kinds of specific information. 

For example, the following query could be used to find only information about data vectors with an attribute 'type' set to 'thermometer'

```
GET /dataVectors/
?include=["id","temperature"]
&criteria={"type":{"equals":"thermometer"}}
```

Return:
```json
[
	{
		"id": "warehouse_thermometer",
		"temperature": 45
	},
	{
		"id": "outsite_thermometer",
		"temperature": 67.34
	}
]
```

However, there are many more filters than can be applied to a specific attribute.

### Equals

Returns all data vectors that have an attribute that is equal to a specified value

```json
{
    "type": {
        "equals": "thermometer"
    }
}
```

### Does Not Equal

Returns all data vectors that have an attribute that is not equal to a specified value

```json
{
    "type": {
        "notequals": "thermometer"
    }
}
```

### Exists

Returns all data vectors that do have an attribute with the specified key, regardless of its value

```json
{
    "temperature": {
        "exists": true
    }
}
```

### Does Not Exist

Returns all data vectors that do have an attribute with the specified key, regardless of its value

```json
{
    "temperature": {
        "exists": false
    }
}
```


### In 

Returns all data vectors that have an attribute with a value in a specified set of values

```json
{
    "temperature": {
        "in": [
            44,
            45,
            46
        ]
    }
}
```
Or
```json
{
    "type": {
        "in": [
            "thermometer",
            "humidifier"
        ]
    }
}
```


### Not In 

Returns all data vectors that have an attribute with a value that is not contained in a specified set of values

```json
{
    "temperature": {
        "notin": [
            44,
            45,
            46
        ]
    }
}
```


### Shortcuts

There are two syntatical shortcuts for 'equals' and 'in' style queries.

#### Quick Equals

This query:
```json
{
    "type": {
        "equals": "thermometer"
    }
}
```
Could be more easily written like this:
```json
{
    "type": "thermometer"
}
```

#### Quick In

This query:
```json
{
    "type": {
        "in": [
            "thermometer",
            "humidifier"
        ]
    }
}
```
Could be more easily written like this:
```json
{
    "type": [
        "thermometer",
        "humidifier"
    ]
}
```