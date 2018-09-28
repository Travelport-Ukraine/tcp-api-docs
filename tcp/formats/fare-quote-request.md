# Fare quote request format

## Format example

```json
{
  "pnr": "CVS6DK",
  "segments": [
    {
      "from": "KBP",
      "to": "CDG",
      "departure": "2019-04-17T06:10:00.000+03:00",
      "arrival": "2019-04-17T08:35:00.000+02:00",
      "airline": "AF",
      "flightNumber": "1653",
      "status": "HK",
      "bookingClass": "Y",
      "isFlown": false,
      "fareBasisCode": "Y3WKWUA9"
    }
  ],
  "passengers": [
    {
      "index": 1,
      "ageCategory": "ADT"
    }
  ],
  "calculationType": "FBC",
  "taxes": [],
  "roe": "1.0",
  "basePrice": "USD646.00",
  "equivalentBasePrice": "EUR558.00",
  "totalPrice": "EUR585.40",
  "fareCalculation": "IEV AF PAR 646.00 NUC646.00",
  "carrier": "AF"
}
```

## Format explanation

| Name | Example | Description |
| :--- | :--- | :--- |
| segments | `Array` | Array of the fare quote segments |
| segments[].index | `1` | Segment index |
| segments[].fareBasis | `'HELLO'` | Segment farebasis |
| segments[].isSaved | `true|false` | Indicates if this is new segment or already saved one |
| segments[].from | `'IEV'` | Segment departure airport |
| segments[].departure | `'2018-09-29T06:50:00.000+02:00'` | Segment departure time |
| segments[].arrival | `'2018-09-29T08:10:00.000+02:00'` | Segment arrival time |
| segments[].airline | `'LH'` | Marketing carrier |
| segments[].flightNumber | `'2282'` | Flight number |
| segments[].bookingClass | `'Y'` | Booking class |
| passengers | `Array` | Array of the fare quote passengers |
| passengers[].index | `1` | Passenger index |
| passengers[].ageCategory | `'ADT'|'CNN'|...` | Passenger type code |
| accountCode | `'ACC'` | Carrier account code |
| currency | `'UAH'|'USD'|...` | Used to set the currency of the fare quote |
| additionalModifiers | `':P'` | Additional fare quote modifiers |
| carrier | `'LH'` | Used for carrier override |
| calculationType | `'FQ'|'FBC'|'FQ.T'|'FQ.H'` | `'FQ'` used for auto fare quote creation, `'FBC'` is used for manual, `FQ.T` and `FQ.H` are used for historical fare quotes creation |
| calculationDate | `'2018-12-01'` | Used for date override for historical fare quotes |
