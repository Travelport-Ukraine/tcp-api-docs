# Authorization and authentication

In order to execute any TCP API method you have to provide `AuthToken` header. `AuthToken` could be obtained after authentication.

For authentication you should use your login and password for TCP.

## Authentication request

### Request endpoint

[https://beta.api.travelcloudpro.eu/auth/login](https://beta.api.travelcloudpro.eu/auth/login)

### Request method

POST

### Request example

```javascript
{
  "username": "tcp-user@travelcloudpro.eu",
  "password": "V3ryS3cr3tP@$$w0rd"
}
```

### Request parameters

| Name | Example | Description |
| :--- | :--- | :--- |
| username | `'tcp-user@travelcloudpro.eu'` | Email used during registration |
| password | `'V3ryS3cr3tP@$$w0rd'` | User password |

### Request headers

No headers required

## Authentication response

### Response example

```javascript
{
  "status": "success",
  "date": "2018-09-28T16:07:17.734Z",
  "requestId": "2018/09/28/[$LATEST]f87b79b2522a4c968d0c1e30d509dbd7\\922f2c8b-c338-11e8-9253-6762b6fcfe83",
  "dataAvailable": true,
  "executionTimeInMs": 290,
  "originalRequest": {
    "username": "tcp-user@travelcloudpro.eu",
    "password": "*"
  },
  "data": {
    "userId": "eu-west-1:efe277f7-e2d9-46ab-b4a8-51cfa3972088",
    "agencyId": "e2ac7bc2-dea6-40b5-b3e7-4285097c73f7",
    "sessionId": "2EMGJT",
    "username": "d.chertousov@gmail.com",
    "availablePccList": [
      "7J8J",
      "79YE",
      "58I4",
      "5JV7",
      "3AQ0",
      "790I",
      "73HJ",
      "5C0L",
      "51ZX"
    ],
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOiJldS13ZXN0LTE6ZWZlMjc3ZjctZTJkOS00NmFiLWI0YTgtNTFjZmEzOTcyMDg4IiwiYWdlbmN5SWQiOiJlMmFjN2JjMi1kZWE2LTQwYjUtYjNlNy00Mjg1MDk3YzczZjciLCJzZXNzaW9uSWQiOiIyRU1HSlQiLCJwY2MiOiI3SjhKIiwiaWF0IjoxNTM4MTUwODM3LCJleHAiOjE1MzgyMzcyMzd9.rMFKdBsZcjXvIplwre6zx39-QUTU5Zr0Cfdsqfs8VHw",
    "pcc": "7J8J",
    "aclRoles": [
      "admin",
      "root"
    ]
  }
}
```

### How to read response

In `data` section of resposne you will find your user and agency information, including list of the PCCs you could switch between, using [ChangePcc](change-pcc.md) method.

Also you will find there `token` field, which contains `AuthToken` you require to authorize your further method calls.

