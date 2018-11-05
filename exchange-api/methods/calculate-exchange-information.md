# CalculateExchangeInformation

`CalculateExchangeInformation` method returns basic information about the difference between ticket and fare quote data, including fare and taxes. It also returns fare quote information with hash if fare quote data was provided to create a new fare quote instead of using saved one.

## CalculateExchangeInformation request

### Request endpoint

[https://beta.api.travelcloudpro.eu/air/exchange/calculate](https://beta.api.travelcloudpro.eu/air/exchange/calculate)

### Request method

POST

### Request example

```javascript
{
  "pnr": "ABCD01",
  "ticketNumber": "0123456789999",
  "fareQuoteData": {
    "segments": [
      {
        "index": 1,
        "fareBasis": null
      },
      {
        "from": "MUC",
        "to": "BRU",
        "departure": "2018-09-29T06:50:00.000+02:00",
        "arrival": "2018-09-29T08:10:00.000+02:00",
        "airline": "LH",
        "flightNumber": "2282",
        "bookingClass": "Y",
        "carrier": "LH",
        "isSaved": false,
        "fareBasis": "",
      }
    ],
    "passengers": [
      {
        "index": 1,
        "ageCategory": "ADT"
      }
    ],
    "accountCode": null,
    "currency": null,
    "additionalModifiers": null,
    "carrier": null,
    "calculationType": "FQ",
    "calculationDate": null
  }
}
```

### Request parameters

| Name | Example | Description |
| :--- | :--- | :--- |
| pnr | `'ABCD01'` | Passenger name record |
| ticketNumber | `'0123456789999'` | Number of the ticket for exchange |
| fareQuoteIndex | `1` | Stored fare quote index. Should be passed either `fareQuoteIndex` or `fareQuoteData` |
| fareQuoteData | `Object` | Object, describing fare quote. See [Fare quote request format](https://github.com/Travelport-Ukraine/tcp-api-docs/tree/a5931a0f9f34859ad45e79139802c8f386f92d64/tcp/formats/fare-quote-request.md) |

### Request headers

| Name | Example | Description |
| :--- | :--- | :--- |
| AuthToken | `'eyJhbGciOiJIUzI1NiIsInR5cCI...'` | Authorization token. See [Authorization and authentication](https://github.com/Travelport-Ukraine/tcp-api-docs/tree/a5931a0f9f34859ad45e79139802c8f386f92d64/tcp/authorization.md) for more details |

## CalculateExchangeInformation response

### Response example

```javascript
{
  "diffBasedOnFare": true,
  "currencyInfo": {
    "ticketBaseCurrency": "USD",
    "baseCurrency": "USD",
    "equivCurrency": "EUR",
    "decimalPlaces": {
      "USD": 2,
      "EUR": 2
    }
  },
  "taxesAdc": {
    "UA": {
      "fareQuote": 0,
      "ticket": 3.45,
      "diff": 0
    },
    "UD": {
      "fareQuote": 0,
      "ticket": 1.73,
      "diff": 0
    },
    "YK": {
      "fareQuote": 0,
      "ticket": 11.22,
      "diff": 0
    },
    "YQ": {
      "fareQuote": 0,
      "ticket": 11,
      "diff": 0
    }
  },
  "basePrice": {
    "fareQuote": 646,
    "ticket": 646,
    "diff": 0
  },
  "adcTotal": 0,
  "refundTotal": 0,
  "fareQuote": {
    "command": null,
    "isAlreadyUpdated": true,
    "source": "terminal",
    "hasNetData": false,
    "index": 1,
    "calculationType": "FB",
    "calculationDate": "2018-09-27",
    "creationDate": "2018-09-27",
    "endorsement": "",
    "pricingInfos": [
      {
        "passengers": [
          {
            "index": 1,
            "lastName": "SURNAME",
            "firstName": "NAMEMR",
            "ageCategory": "ADT",
            "status": "B",
            "amount": "EUR558.00",
            "isTicketed": false
          }
        ],
        "fareCalculation": "IEV AF PAR 646.00 NUC646.00",
        "roe": "1.0",
        "baggage": [
          {
            "amount": 0,
            "units": "piece"
          }
        ],
        "segments": [
          {
            "index": 1,
            "fareBasisCode": "Y3WKWUA9",
            "baggage": {
              "amount": 0,
              "units": "piece"
            },
            "notValidBefore": "2019-04-15",
            "notValidAfter": "2019-04-15"
          }
        ],
        "totalPrice": "EUR558.00",
        "basePrice": "USD646.00",
        "taxes": "EUR0.00",
        "taxesInfo": [],
        "equivalentBasePrice": "EUR558.00"
      }
    ],
    "it": false,
    "bt": false,
    "segments": [
      {
        "index": 1,
        "isFlown": false,
        "airline": "AF",
        "flightNumber": "1653",
        "bookingClass": "Y",
        "from": "KBP",
        "to": "CDG",
        "status": "HK1",
        "departure": "17APR",
        "departureTime": "0610",
        "arrival": "17APR",
        "arrivalTime": "0835"
      }
    ],
    "passengersIndexes": [
      1
    ],
    "platingCarrier": "AF",
    "hash": "9aa9a825d4ae813b79b8b163845d898e",
    "screen": "FB1  - S1                                         27SEP18 WS/AG\n P1  SURNAME/NAMEMR            ADT   B             EUR  558.00 \n IEV AF PAR 646.00 NUC646.00END ROE1.0                         \n FARE USD646.00 EQU EUR558.00 TOT EUR558.00                    \n              ***ADDITIONAL FEES MAY APPLY*SEE>FO1;            \n S1   FB-Y3WKWUA9         B-0PC  NB-15APR  NA-15APR            \n T P1/S1/CAF                                                   \n><",
    "fareBasisValidationWarnings": []
  },
  "equivalentBasePrice": {
    "fareQuote": 558,
    "ticket": 550,
    "diff": 0
  }
}
```

### How to read response

* `diffBasedOnFare` indicates if difference is calculated based on fare or equivalent fare.
* `currencyInfo` provides information about ticket and fare quote currencies, along with decimal places for this currencies in the current market
* `taxesAdc` section contains information about the taxes values and the calculated diff
* `basePrice` indicated base price values and the diff
* `equivalentBasePrice` indicated equivalent base price values and the diff
* `adcTotal` and `refundTotal` indicated current value of prognosed additional collection and refund based on current taxes and fare values if no penalty is provided
* `fareQuote` field holds information about the fare quote which has been created using the data provided

