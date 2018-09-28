# Involuntary rerouting

Involuntary rerouting is a special exchange case, caused by the carrier. No penalties could be provided in this case and no commission could be collected by the agent, so it's getting easier to process an exchange, eliminating some complex calculations.

## Involuntary rerouting procedure

### 1. Get your PNR

Run [GetBooking](../tcp/get-booking.md) request. You will need `segments` and `passengers` section of the response.

#### Example response
```json
{
  "type": "uAPI",
  "pnr": "ABCD01",
  "version": "6",
  "uapi_ur_locator": "ABCD02",
...
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
...
  "passengers": [
    {
      "lastName": "NAMEMR",
      "firstName": "SURNAME",
      "uapi_passenger_ref": "coVt5Wcc1BKAQQ/KTLAAAA==",
      "index": 1,
      "ageCategory": "ADT"
    }
  ],
}
```

If some segments were added by the airline, make sure you have changed their status to HK. If no, you have to add segments by yourself like it's covered in the next step.


### 2. Add segments to PNR

This step is not necessary if the carrier has already added them and you successfully updated their status to HK.

You can add segments manually or pass them in appropriate format to the [CalculateExchangeInformation](./calculate-exchange-information.md) method.

### 3. Get your ticket information

Use [GetTicket](../tcp/get-ticket.md) method to acquire ticket information as you will use it during exchange.

You will need `endorsement` and `basePrice` and `equivalentBasePrice` fields from the method response in order to process an exchange.

### 4. Get a quote

You should get an exchange quote using segments selected for exchange. Use [CalculateExchangeInformation](./calculate-exchange-information.md) method for this.

You will use method response during exchange.

### 5. Process an exchange

You will have to run [ExchangeTicket](./exchange-ticket.md) method providing information from the previous steps.

#### Example request

```json
{
  "pnr": "ABCD01",
  "ticketNumber": "0123456789999",
  "fareQuoteData": {
    "segments": [
      {
        "from": "KBP",
        "to": "CDG",
        "airline": "AF",
        "flightNumber": "1653",
        "serviceClass": "Economy",
        "index": 1,
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
  },
  "fareQuoteHash": "9aa9a825d4ae813b79b8b163845d898e",
  "exchangeData": {
    "adcTotal": 0,
    "refundTotal": 0,
    "refundFare": false,
    "fareQuote": {
      "basePrice": 999,
      "endorsement": "NEW ENDORSEMENT",
      "taxes": {}
    },
    "it": false,
    "bt": false,
    "tourCode": "TC",
    "commission": {
      "type": "Z",
      "value": 0
    },
    "penaltyData": {
      "type": "absent",
      "data": {}
    },
  }
}
```

#### How to build a request

* In `pnr` and `ticketNumber` fieldsyou should indicate correspondent PNR and ticket number
* `fareQuoteData` field is a `fareQuote` field of the `CalculateExchangeInformation` method response
* `fareQuoteDataHash` - is a field `fareQuote.hash` field of the `CalculateExchangeInformation` method response. I helps to ensure that the very same fare quote will be created during exchange
* `exchangeData` is the field which contains a structure with all the exchange settings
  * `adcTotal` and `refundTotal` should be set to `0` in case of involuntary exchange
  * `refundFare` should be set to `false`
  * `fareQuote` attribute describes required changes to the fare quote that will be created
    * `basePrice` should be set to the numeric value of ticket's `basePrice`
    * `endorsement` should contain original ticket endorsement with an addition of any text, required by the carrier
    * `taxes` should be set to empty object in case of involuntary rerouting
  * `it` and `bt` fields should be set to the `true` or `false` based on the tickets value
  * `tourCode` field should be copied from ticket or set to `null`
  * `commission` should have type `Z` and value `0` in case of involuntary rerouting
  * `penaltyData` should have `type` set to `absent` and `data` to empty object

You may also pass `copyOptions` param if you need to apply same exchange process to several passengers.

See [ExchangeTicket](./exchange-ticket.md) method documentation for more information.

### 6. Finish exchange by issung ticket

Use [ExchangeTicket](./exchange-ticket.md) method response to extract filed fares indexes to be issued.

To finish exchange you should use [FinishExchange](./finish-exchange.md) method.


### 7. Clean everything up

Don't forget to remove old segments. You may use [RemoveSegment](../tcp/remove-segment.md) method for this purpose.

