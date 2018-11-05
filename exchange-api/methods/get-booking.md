# GetBooking

GetBooking method is used to acquire information about the PNR.

## GetBooking request

### Request endpoint

[https://beta.api.travelcloudpro.eu/core/booking/{pnr}](https://beta.api.travelcloudpro.eu/core/booking/{pnr})

### Request method

GET

### Request parameters

| Name | Example | Description |
| :--- | :--- | :--- |
| pnr | `'ABCD01'` | Passenger name record |

### Request headers

| Name | Example | Description |
| :--- | :--- | :--- |
| AuthToken | `'eyJhbGciOiJIUzI1NiIsInR5cCI...'` | Authorization token. See [Authorization and authentication](../exchange/authorization.md) for more details |

## GetBooking response

### Response example

```javascript
{
  "type": "uAPI",
  "pnr": "ABCD01",
  "version": "6",
  "uapi_ur_locator": "0HW9WB",
  "uapi_reservation_locator": "79RCF5",
  "airlineLocatorInfo": [
    {
      "createDate": "2018-09-13T12:35:00.000+00:00",
      "supplierCode": "AF",
      "locatorCode": "QI59EG"
    }
  ],
  "createdAt": "2018-09-13T12:36:55.647+00:00",
  "hostCreatedAt": "2018-09-13",
  "modifiedAt": "2018-09-27T13:43:06.732+00:00",
  "fareQuotes": [],
  "segments": [
    {
      "from": "KBP",
      "to": "CDG",
      "group": 0,
      "departure": "2019-04-17T06:10:00.000+03:00",
      "arrival": "2019-04-17T08:35:00.000+02:00",
      "airline": "AF",
      "flightNumber": "1653",
      "uapi_segment_ref": "5w/fCYBAAA/BUoFPaLAAAA==",
      "serviceClass": "Economy",
      "plane": [
        "320"
      ],
      "duration": [
        "205"
      ],
      "techStops": [],
      "index": 1,
      "status": "HK",
      "bookingClass": "Y",
      "isFlown": false
    }
  ],
  "serviceSegments": [],
  "passengers": [
    {
      "lastName": "SURNAME",
      "firstName": "NAMEMR",
      "uapi_passenger_ref": "coVt5Wcc1BKAQQ/KTLAAAA==",
      "index": 1,
      "ageCategory": "ADT"
    }
  ],
  "emails": [],
  "bookingPCC": "58I4",
  "tickets": [
    {
      "number": "0579903116953",
      "passengers": [
        {
          "firstName": "NAMEMR",
          "lastName": "SURNAME"
        }
      ],
      "uapi_passenger_ref": "coVt5Wcc1BKAQQ/KTLAAAA==",
      "uapi_pricing_info_ref": null
    },
    {
      "number": "0579903116954",
      "passengers": [
        {
          "firstName": "NAMEMR",
          "lastName": "SURNAME"
        }
      ],
      "uapi_passenger_ref": "coVt5Wcc1BKAQQ/KTLAAAA==",
      "uapi_pricing_info_ref": null
    }
  ]
}
```

