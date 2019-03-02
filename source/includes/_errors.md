# Errors

Errors are the logs that is sent from the client when window.onerror is invoked.
There are several ways that can result in errors like this.

1. The client tried to access inaccessible memory location
2. Bad code in the client app

The endpoint responsible for handling the errors from the clients is /analytics/errors

## Get Errors

```shell
  curl "http://167.99.164.204/api/v1/analytics/error"
    -X "GET"
    -H "Authorization: thanosrocks"
```

```javascript
  fetch("http://167.99.164.204/api/v1/analytics/error")
    .then(data => data.json())
    .then(d => {
      // process data here
      console.log(d);
    })
```

> The above command returns JSON structured like this:

```json
  [
    {
      "timestamp": "Mon, 25 Feb 2019 08:15:15 GMT",
      "session_id": 123,
      "code": 101,
      "severity": "FATAL",
      "msg": "Mon, 25 Feb 2019 08:15:15 GMT: FATAL code 101 unable to render proper information"
    },
  ]
```

This endpoint list the errors that is logged from the server, ordered by the timestamp from the latest to the earliest errors.

### HTTP Request

`GET /api/v1/analytics/error`

## Post Errors

This endpoint receives the errors sent from the client and stores it to the database.
Please note that the error messages is parsed directly from `window.onerror` function.

```shell
  curl "http://167.99.164.204/api/v1/analytics/error"
    -X "POST"
    -H "Authorization: thanosrocks"
    -d "Thu, 28 Feb 2019 22:46:59 GMT on file http://167.99.164.204/testsite/ line 20 col 11: Uncaught ReferenceError: boom is not defined"
```

```javascript
  fetch("http://167.99.164.204/api/v1/analytics/error", {
    method: "POST",
    body: "Thu, 28 Feb 2019 22:46:59 GMT on file http://167.99.164.204/testsite/ line 20 col 11: Uncaught ReferenceError: boom is not defined",
  })
    .then(data => data.json())
    .catch(err => {
      // retries here
    })
```

> The above command returns JSON structured like this:

```json
  [
    {
      "timestamp": "Mon, 25 Feb 2019 08:15:15 GMT",
      "session_id": 123,
      "code": 101,
      "severity": "FATAL",
      "msg": "Thu, 28 Feb 2019 22:46:59 GMT on file http://167.99.164.204/testsite/ line 20 col 11: Uncaught ReferenceError: boom is not defined"
    },
  ]
```

### HTTP Request

`POST /api/v1/analytics/error`

