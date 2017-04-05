Data Vectors
=============

Data vectors are logical entities that represent an aggregation point for a given channel of information. They are modeled as documents.


### GET /dataVectors/
List all existing data vectors

Parameters

   * include - An array of attributes to return. If none are specified, only 'id' is returned
   * criteria - An object containing attributes to filter the results by. For additional information, see [Query Operators](Query%20Operators.md)
   * pagination - An object that contains the current page index and length
   * sort - An object containing the attribute to sort by, and direction

```
GET /dataVectors/
?include=["id","temperature"]
&criteria={"type":"thermometer"}
&pagination={"index":5,"length":2}
&sort={"attribute":"temperature","direction":"ascending"}
```

Return:
```json
[
	{
		"id": "warehouse_thermometer",
		"temperature": 45
	},
	{
		"id": "data vector",
		"temperature": 67.34
	}
]
```

### GET /dataVectors/:identifier
Retrieve the full state of a data vector with the specified identifier.

Parameters

   * include - An array of attributes to return. If none are specified, all attributes are returned


```
GET /dataVectors/warehouse_thermometer&include=["id","temperature","humidity"]
```
Return:
```json
{
	"id": "warehouse_thermometer",
	"temperature": 45,
	"humidity": 22
}
```


### POST /dataVectors/:identifier
Update a data vector with the specified identifier. If one does not yet exist, it will be created with the specified data.
```
POST /dataVectors/warehouse_thermometer
```
```json
{
	"temperature": 88
}
```
There is no return data for this call.


### POST /dataVectors/
Create a new data vector, with all attributes specified in the body. An identifier will be returned to the user.
```
POST /dataVectors/
```
```json
{
	"temperature": 45
}
```
Return
```json
{
	"id": "wgsdf7q234nasdf"
}
```



### DELETE /dataVectors/:identifier

Delete a data vector with the specified identifier. If no data vector with that identifier is found, return an error. Otherwise, return nothing.
```
DELETE /dataVectors/warehouse_thermometer
```
There is no return data for this call.
