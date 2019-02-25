# Logs

Logs are visit information that is stored in the database. it consists of
the following fields

Field | Description
----- | -----------
id | The ID of the log
timestamp | The timestamp visited
session_id | The session_id of the visitor
endpoint | The endpoint visited


## Get logs

```shell
  curl "http://167.99.164.204/api/v1/analytics/logs"
    -X "GET"
    -H "Authorization: thanosrocks"
```

> The above command returns JSON structured like this:

```json
  {
    "id": 0,
    "timestamp": "Mon, 25 Feb 2019 08:15:15 GMT",
    "session_id": 123,
    "endpoint": "/",
  }
```

This endpoint retrieves raw JSON formatted logs.

### HTTP Request

`GET "http://http://167.99.164.204/api/v1/analytics/logs/<limit>"`


### URL Parameters
Parameter | Description
--------- | -----------
limit | the latest `limit` logs, max=500

## Post logs

```shell
  curl "http://167.99.164.204/api/v1/analytics/logs"
    -X "POST"
    -H "Authorization: thanosrocks"
    -d 'Mon, 25 Feb 2019 08:15:15 GMT Logged /endpoint'
```


> The above command returns JSON structured like this:

```json
  {
    "id": 1,
    "timestamp": "Mon, 25 Feb 2019 08:15:15 GMT",
    "session_id": 123,
    "endpoint": "/endpoint",
  }
```

This endpoint receive logs that is sent from the user client.

### HTTP Request

`POST "http://http://167.99.164.204/api/v1/analytics/logs/"`


### Query Parameters
Parameter | Description
--------- | -----------
msg | The log message as a string text.