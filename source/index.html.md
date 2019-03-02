---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - javascript

toc_footers:
  - <a href='#'>Documentation Powered by Infinity Stones</a>

includes:
  - database
  - bcc
  - logs
  - errors

search: true
---

# Introduction

Welcome to CSE 135 analytics web application, we call this app Endgame because 
why not ?!

The app is built on NodeJS with MySQL as the DMS. It features analytics dashboard that allows user to see the necessary information about user activities in the [Test Site](https://facebook.com). Those information will include the following:

1. Basic Client Characteristic
2. Speed Characteristic
3. Errors
4. Events

For user authentication, we use [Passport](http://www.passportjs.org/). Specifically we use `passport-local` strategy connected with user database. User's password will be encrypted using usual SHA256 encryption procedure.

## Dashboard Access

You will need access to the dashboard. The default user will be the following

Field | Value
----- | -----
username | grader
password | helloworld

## API Key Access

There are no API key generation endpoints for now, we use static key that must be included in the header as Authorization field. The API key can be found [here](https://github.com/albertputrapurnama/endgame-server) on the readme.

# Authentication

> Make sure to replace `thanosrocks` with your API key.

```shell
  curl "api_endpoint_here"
    -H "Authorization: thanosrocks"
```

```javascript
  fetch("api_endpoint_here", {
    headers: {
      'Authorization': "thanosrocks"
    }
  }).then((res) => {
    // do something here
  }).catch((err) => {
    // err handling here
  })
```

Endgame uses API keys to allow access to the API. You can get Endgame API key [here](https://github.com/albertputrapurnama/endgame-server).

Endgame expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: thanosrocks`

<!-- <aside class="notice">
You must replace <code>thanosrocks</code> with your personal API key.
</aside> -->
<aside class="notice"> Authentication still in development mode. You do not need to use Authorization header to use the API endpoints </aside>