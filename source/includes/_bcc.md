# BCC

**Basic Client Characteristics** is the endpoint that is responsible for collecting and parsing the user's browser information. The task includes:

1. Parsing client's User Agent header.
2. Get the window information.
3. Get the IP address (on progress).
4. Record necessary browser's information in the database.

Furthermore, this endpoint provides a way to read the client characteristics from the database.

## Get BCCs

```shell
  curl "http://167.99.164.204/api/v1/analytics/bcc"
    -X "GET"
    -H "Authorization: thanosrocks"
```

```javascript
  fetch("http://167.99.164.204/api/v1/analytics/bcc")
    .then(data => data.json())
    .then(data => {
      // parse data and rendering here
    })
    .catch(err => {
      // retries here
    })
```

> The above command returns JSON structured like this:

```json
  [
    {
        "id": 1,
        "session_id": "s%3AM7qh_iUtflV7IihSxfWXfUDr2Tcjq9_8.JcvA206%2FFyn%2FPfNBpak6gvPC3irutgdvPmK8Y%2F8DhvI",
        "timestamp": "Wed, 27 Feb 2019 21:01:30 GMT",
        "device_type": null,
        "browser_type": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/72.0.3626.119 Safari/537.36",
        "screen_height": 1050,
        "screen_width": 1680,
        "geo_location": null
    },
    {
        "id": 14,
        "session_id": "s%3A4pkaxRT94isQbtd7Y4USAUQCiMpT7YEz.wyBNWU8Y%2F6FhBvpX2ODuQUIEJTqQYIiW3RcRb%2B3SRNA",
        "timestamp": "Thu, 28 Feb 2019 22:49:01 GMT",
        "device_type": null,
        "browser_type": "Mozilla/5.0 (iPhone; CPU iPhone OS 11_0 like Mac OS X) AppleWebKit/604.1.38 (KHTML, like Gecko) Version/11.0 Mobile/15A372 Safari/604.1",
        "screen_height": 812,
        "screen_width": 375,
        "geo_location": null
    },
  ]
```

This endpoint reads the database and compile it into a JSON formatted payload for the client to parse and load to their page views. 

### HTTP Request

`GET /api/v1/analytics/bcc`

## Post BCCs

This endpoint is responsible in parsing, creating the client characteristic information and then recording the information into the database for developers to analyze.

### HTTP Request

```shell
  curl "http://167.99.164.204/api/v1/analytics/bcc"
    -X "POST"
    -H "Authorization: thanosrocks"
    -d "<json-stringified-payload>"
```

```javascript
  fetch("http://167.99.164.204/api/v1/analytics/bcc", {
    method: "POST",
    credentials: "includes",
    body: {
      "session_id": 123,
      "timestamp": "Thu, 28 Feb 2019 22:49:01 GMT",
      "browser_type": "Mozilla/5.0 (iPhone; CPU iPhone OS 11_0 like Mac OS X) AppleWebKit/604.1.38 (KHTML, like Gecko) Version/11.0 Mobile/15A372 Safari/604.1",
      "screen_height": 1050,
      "screen_width": 1680
    }
  })
    .then(data => data.json())
    .then(data => {
      // parse data and rendering here
    })
    .catch(err => {
      // retries here
    })
```

> The above command returns a `204` status code when it's successfully accepted by the server.

`POST /api/v1/analytics/bcc`

The request body should contain JSON which has the informations of the client's browser

### Payload

Parameter | Description | Type | Required
--------- | ----------- | ---- | --------
session_id | The user's session_id | string | YES
timstamp | The UTC timestamp where the user visited the website | string | YES
browser_type | The User Agent of the browser | string | YES
screen_height | The device screen height | int | YES
screen_width | The device screen width | int | YES

<aside class="notice">
  You will notice that while all the payload parameters are required, if you left any of them empty, the endpoint will still work because it does not have a input type checker on the server side. This will cause an incomplete dataset which can be cleared later on.
</aside>

