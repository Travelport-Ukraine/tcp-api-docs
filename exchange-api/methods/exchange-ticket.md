# ExchangeTicket

`ExchangeTicket` method processes the most intensive work about exchange. It creates and updates fare quote according to all provided fare quote, ticket, penalty, commission and other data. It tuns through the exchange process and ends up with the fare quote ready to be issued.

## ExchangeTicket request

### Request endpoint

[https://beta.api.travelcloudpro.eu/air/exchange/process](https://beta.api.travelcloudpro.eu/air/exchange/process)

### Request method

POST

### Request example

```javascript
{
  "pnr": "ABCD01",
  "ticketNumber": "0123456789999",
  "suppressFareBasisValidationWarnings": false,
  "fareQuoteData": {
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
  },
  "fareQuoteHash": "9aa9a825d4ae813b79b8b163845d898e",
  "exchangeData": {
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
}
```

### Request parameters

| Name | Example | Description |  |
| :--- | :--- | :--- | :--- |
| pnr | `'ABCD01'` | Passenger name record |  |
| ticketNumber | `'0123456789999'` | Number of the ticket for exchange |  |
| suppressFareBasisValidationWarnings | \`true | false\` | Should be passed as true, if fare basis validation warnings were returned while creating fare quote |
| fareQuoteIndex | `1` | Stored fare quote index. Should be passed either `fareQuoteIndex` or `fareQuoteData` |  |
| fareQuoteData | `Object` | Object, describing fare quote. See [Fare quote request format](https://github.com/Travelport-Ukraine/tcp-api-docs/tree/a5931a0f9f34859ad45e79139802c8f386f92d64/tcp/formats/fare-quote-request.md) |  |
| fareQuoteHash | `'9aa9a825d4ae813b79b8b163845d898e'` | Should be passed along with `fareQuoteData` to verify its integrity during exchange process |  |
| fareQuoteIndex | `1` | Stored fare quote index. Should be passed either `fareQuoteIndex` or `fareQuoteData` |  |
| exchangeData | `Object` | Object, describing exchange options. See [Exchange data request format](https://github.com/Travelport-Ukraine/tcp-api-docs/tree/a5931a0f9f34859ad45e79139802c8f386f92d64/tcp/formats/exchange-data-request.md) |  |

### Request headers

| Name | Example | Description |
| :--- | :--- | :--- |
| AuthToken | `'eyJhbGciOiJIUzI1NiIsInR5cCI...'` | Authorization token. See [Authorization and authentication](https://github.com/Travelport-Ukraine/tcp-api-docs/tree/a5931a0f9f34859ad45e79139802c8f386f92d64/tcp/authorization.md) for more details |

## ExchangeTicket response

### Response example

```javascript
[
  {
    "status": "PREPARED_FQ",
    "exchangeScreens": [
      {
        "exchangeStep": "EXCHANGE_STEP_RESOLVE_FQ",
        "screen": "FB1  - S1                                         27SEP18 WS/AG\n P1  SURNAME/NAMEMR            ADT   B             EUR  558.00 \n IEV AF PAR 646.00 NUC646.00END ROE1.0                         \n FARE USD646.00 EQU EUR558.00 TOT EUR558.00                    \n              ***ADDITIONAL FEES MAY APPLY*SEE>FO1;            \n S1   FB-Y3WKWUA9         B-0PC  NB-15APR  NA-15APR            \n NONREF -NO CHANGE-NONREF - NO CHANGE                          \n T P01/S1/Z0/FEX0123456789999/CAF                              \n><"
      },
      {
        "exchangeStep": "EXCHANGE_STEP_TICKET",
        "command": "*EX **TICKET FOR**: SURNAME/NAMEMR                PSGR  1/ 1\n  NEW FARE: USD    646.00  EQUIV:;EUR   558.00                 \nTX1:     0.00   TX2:     0.00   TX3:     0.00   TX4:     0.00  \n\n *EXCH TICKET*: TICKET NUMBER   THRU  TICKET NUMBER  NO. CPNS\n               ;01234567899990  ;.   ;..............   ;01\n  COUPONS FOR  TKT1:;1...   TKT2:;....  TKT3:;....  TKT4:;....\n TTL VALUE:;EUR558.00... BSR:;...... ORIG FOP:;S.............. \n *ORIG ISSUE*: TICKET NUMBER   ORG/DES  CITY  DATE   IATA CODE\n              ;.............. ;KBP/CDG  ;KIV ;13SEP18 ;9999999\n;",
        "screen": ">*EX **TICKET FOR**: SURNAME/NAMEMR                PSGR  1/ 1\n  NEW FARE: USD    646.00  EQUIV:;EUR   558.00                 \nTX1:     0.00   TX2:     0.00   TX3:     0.00   TX4:     0.00  \n\n *EXCH TICKET*: TICKET NUMBER   THRU  TICKET NUMBER  NO. CPNS\n               ;01234567899990  ;.   ;..............   ;01\n  COUPONS FOR  TKT1:;1...   TKT2:;....  TKT3:;....  TKT4:;....\n TTL VALUE:;EUR550.00... BSR:;...... ORIG FOP:;S.............. \n *ORIG ISSUE*: TICKET NUMBER   ORG/DES  CITY  DATE   IATA CODE\n              ;.............. ;KBP/CDG  ;KIV ;13SEP18 ;9999999\n;\n><"
      },
      {
        "exchangeStep": "EXCHANGE_STEP_TAXES",
        "command": "*TP **TICKET FOR**: SURNAME/NAMEMR                PSGR  1/ 1\n  NEW FARE: USD    646.00  EQUIV:;EUR   558.00                 \nTX1:     0.00   TX2:     0.00   TX3:     0.00   TX4:     0.00  \nPAID TAXES\nT1 ;11.00...;YQ T2 ;11.22...;YK T3 ;1.73....;UD T4 ;3.45....;UA\nT5 ;........;.. T6 ;........;.. T7 ;........;.. T8 ;........;..\nT9 ;........;.. T10;........;.. T11;........;.. T12;........;..\nT13;........;.. T14;........;.. T15;........;.. T16;........;..\nT17;........;.. T18;........;.. T19;........;.. T20;........;..\n\nU.S. PSGR FACILITY CHARGES\nAPT1 ;...;..... APT2 ;...;..... APT3 ;...;..... APT4 ;...;..... \n;",
        "screen": ">*TP **TICKET FOR**: SURNAME/NAMEMR                PSGR  1/ 1\n  NEW FARE: USD    646.00  EQUIV:;EUR   558.00                 \nTX1:     0.00   TX2:     0.00   TX3:     0.00   TX4:     0.00  \nPAID TAXES\nT1 ;3.45....;UA T2 ;1.73....;UD T3 ;11.22...;YK T4 ;11.00...;YQ\nT5 ;........;.. T6 ;........;.. T7 ;........;.. T8 ;........;..\nT9 ;........;.. T10;........;.. T11;........;.. T12;........;..\nT13;........;.. T14;........;.. T15;........;.. T16;........;..\nT17;........;.. T18;........;.. T19;........;.. T20;........;..\n\nU.S. PSGR FACILITY CHARGES\nAPT1 ;...;..... APT2 ;...;..... APT3 ;...;..... APT4 ;...;..... \n;\n><"
      }
    ],
    "exchangeDetails": {
      "fq": {
        "command": null,
        "isAlreadyUpdated": true,
        "source": "terminal",
        "hasNetData": false,
        "index": 1,
        "calculationType": "FB",
        "calculationDate": "2018-09-27",
        "creationDate": "2018-09-27",
        "endorsement": "NONREF -NO CHANGE-NONREF - NO CHANGE",
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
          1
        ],
        "passengersIndexes": [
          1
        ],
        "commission": {
          "percent": 0
        },
        "platingCarrier": "AF",
        "formOfPayment": "EX0123456789999",
        "exchangedFor": "0123456789999",
        "hash": "9aa9a825d4ae813b79b8b163845d898e",
        "screen": "FB1  - S1                                         27SEP18 WS/AG\n P1  SURNAME/NAMEMR            ADT   B             EUR  558.00 \n IEV AF PAR 646.00 NUC646.00END ROE1.0                         \n FARE USD646.00 EQU EUR558.00 TOT EUR558.00                    \n              ***ADDITIONAL FEES MAY APPLY*SEE>FO1;            \n S1   FB-Y3WKWUA9         B-0PC  NB-15APR  NA-15APR            \n NONREF -NO CHANGE-NONREF - NO CHANGE                          \n T P01/S1/Z0/FEX0123456789999/CAF                              \n><"
      },
      "emdData": null
    }
  }
]
```

