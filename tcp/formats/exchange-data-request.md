# Exchange data request format

## Format example

```json
{
  "adcTotal": 0,
  "refundTotal": 0,
  "refundFare": false,
  "fareQuote": {
    "basePrice": 646,
    "endorsement": "NONREF -NO CHANGE-NONREF - NO CHANGE",
    "taxes": {}
  },
  "it": false,
  "bt": false,
  "tourCode": null,
  "refundTaxes": null,
  "commission": {
    "type": "Z",
    "value": 0
  },
  "formOfPayment": null,
  "penaltyData": {
    "type": "absent",
    "data": {}
  }
}
```

## Format explanation

| Name | Example | Description |
| :--- | :--- | :--- |
| adcTotal | `100` | Expected additional collection during exchange |
| refundTotal | `300` | Expected refund value during exchange |
| refundFare | `true|false` | Indicates if fare should be refunded during exchange |
| fareQuote | `Object` | Describes changes, required to be provided to the fare quote during the exchange |
| it | `true|false` | IT modifier |
| bt | `true|false` | BT modifier |
| tourCode | `'LEISURE'` | Sets tour code to the fare quote, should be passed if tour code is required |
| refundTaxes | `Array` | Contains array of taxes, which should be refunded with corresponding values |
| commission | `Object` | Comission object |
| commission.type | `'Z'|'ZA'` | `'Z'` - percent commission type, `'ZA'` -absolute commission type |
| commission.value | `10` | Commission value |
| formOfPayment | `Array` | Describes up to three form of payment in case of additional collection |
| penaltyData | `Object` | Describes penalty data for exchange. See [Penalty format](./penalty.md) for details |




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
