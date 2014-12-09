Data Vectors
=============

Data vectors are logical entities that represent an aggregation point for a given channel of information.


## /dataVectors/create/

Create a new data vector in the platform. Returns the ID of the newly created data vector, or failure.

Input Variables

   * Name - A name for the new data vector
   * Attributes - Key value pairs
   		* Connector pairs - A list of key-value pairs of information. Only used by the realtime data input API to allow easier association between incoming information and a data vector. Optional.

Input
```json
{
   "authentication": { },
   "data": {
      "name": "New Data Vector",
      "attributes": {
         "attribute1": "value1",
         "temperature": 45.00,
         "connectors": [
            {
                "type": "rfid",
                "id": "12345"
            }
      	]
      }
   }
}
```

Return:
```json
{
   "session": {
      "valid": true,
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

## /dataVectors/update/

Update an existing data vector.

Input Variables

   * Attributes - Key value pairs
   * Connector - A Key/value pair used to correlate the event with an existing data vector. Optional.
   * ID - The data vector ID. Optional, unless 'connector' is not specified

Input
```json
{
   "authentication": { },
   "data": {
      "connector": {
            "type": "rfid",
            "id": "12345"
      },
      "attributes": {
         "temperature": 72.23,
      }
   }
}
```

Return:
```json
{
   "session": {
      "valid": true,
      "expiration": {
         "expires": 1381349923,
         "validFor": 1997693
      }
   },
   "status": {
      "description": "Everything went as planned.",
      "success": true,
      "time": 1379352230
   },
   "data": {
      "valid": true
   }
}
```
