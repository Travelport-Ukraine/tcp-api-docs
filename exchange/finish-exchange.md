# FinishExchange

`FinishExchange` method is used to issue tickets and all appropriate documents in order to finish exchange.

## FinishExchange request

### Request endpoint

https://beta.api.travelcloudpro.eu/air/exchange/finish

### Request method

POST

### Request example

```json
{
  "pnr": "ABCD01",
  "fareQuoteIndex": 1,
  "printEmd": false
}
```

### Request parameters

| Name | Example | Description |
| :--- | :--- | :--- |
| pnr | `'ABCD01'` | Passenger name record |
| fareQuoteIndex | `1` | Index of the fare quote to issue ticket with |
| printEmd | `true|false` | Indicates if the penalty EMD, associated with this exchange should be issued along with a ticket |

### Request headers

| Name | Example | Description |
| :--- | :--- | :--- |
| AuthToken | `'eyJhbGciOiJIUzI1NiIsInR5cCI...'` | Authorization token. See [Authorization and authentication](../tcp/authorization.md) for more details |


## FinishExchange response

### Response example

```json
{
  "ticket": {
    "ticketNumber": "0579903116968"
  }
}
```
