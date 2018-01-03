# Fly From with options API

Provides the lowest price for a selection of destinations from predefined departure point.

## Fly From with options request

### Sample request \(type: GET\)

> [https://api.travelcloudpro.eu/v1/cache/flyfrom?origin=IEV&pointOfSale=UA&destination=PRG,WAW,BRU&minDepartureDate=2017-11-01&maxDepartureDate=2017-11-07&minStay=5&maxStay=10](https://api.travelcloudpro.eu/v1/cache/flyfrom?origin=IEV&pointOfSale=UA&destination=PRG,WAW,BRU&minDepartureDate=2017-11-01&maxDepartureDate=2017-11-07&minStay=5&maxStay=10)

### Request parameters

The following table illustrates the minimum required data for Fly From API with Options request.

| Name | Example | Description |
| :--- | :--- | :--- |
| pointOfSale | UA | Country ISO code where shopping request was generated |
| minDepartureDate | 2017-01-01 | The earliest possible journey departure date |
| maxDepartureDate | 2017-01-07 | The farthest possible journey departure date |
| origin | IEV | City IATA code where the journey begins \(do not use airport code\) |
| destination | PRG,WAW,BRU | City IATA code where the journey ends\(do not use airport code\) |
| minStay | 5 | Minimum number of days which should be spent at the point of destination before return journey |
| maxStay | 10 | Maximum mumber of days to be spent at the poing of destination before return journey |

## Fly From with options response

### Response sample \(application/json\)

```js
{
    "status": "success",
    "dataAvailable": true,
    "requestId": "fe3cf313-0e4c-11e7-b9ff-711858ad153a",
    "executionTimeInMs": 238,
    "originalRequest": {
        "origin": "IEV",
        "pointOfSale": "UA",
        "destination": "PRG,WAW,BRU",
        "minDepartureDate": "2017-11-01",
        "maxDepartureDate": "2017-11-07",
        "minStay": "5",
        "maxStay": "10"
    },
    "data": {
        "proposalsCount": 3,
        "compressedDataSize": 472,
        "base64GzippedResponse": "H4sIAAAAAAAAA7XUS4vbMBAA4P+is2M0o5elWza7bZZsaEidLrTswcTeIEht6jiFEvzfO2oDeeCkDqTgw3hsSaOPkXbsdfjK3I49+rpYNiHKvlfbkiK0gkdsua3rolz+Yo4thmMWsZ/Z2udZ48vVKKtrX9T0ZfaZPlS1X/kyW8+LH9tiQxMw5GAAuHp++kKr/H0DTiElaMCmyWhaFbF1tmmmVe7ffZHvhw04DgBT0E4pJ2ycWP2VhlCNVZ0PV8VzOd0wJ8CiBG6QCl0XK8p82+3roHkmDzMaklMtVFbjq5ALu22jo59C4vynMLB9ayM2qsqSVEJVBxdpBPZ0eRlfczEnLuLMRV9wEQNuUp44SBya2Ere4QIoNErURv8PF4KZzT92N43SqHvifJpcw5FkQavscZDCY5zkIg7wPzjWCRmD7GoaazQ90vTumbDZE5uQuK1nFKDqyTL8cI0Fjll4csZiLrOYlEykdAgxt9B1lgTNZ1Wo8/4s5PIwX3S3TAIS7nLPhJahVfYtAxT2tNEpN05JByrW2nbYSM25lVaavjZhsyc2IXHjNaNl3+t38vKva+bAos5YLp8khBQEHSOHgli6TpLRibaq9zm6BaVtfwOK5+X6mgYAAA=="
    }
}
```

### Response parameters

Please find below response elements for FlyFrom with Options API:

| Name | Data type | Description |
| :--- | :--- | :--- |
| status | string | Can be "success" or "error". Indicates an error while validating input params and while processing warehouse response. If the status is "error" then errorMessage is provided |
| dataAvailable | boolean | If value false is returned data is not avialable either because too distant dates indicated or some mandatory parameters not specified. In the latter case errorMessage is provided |
| requestId | string | Provides id for a API call |
| executionTimeInMs | number | Indicates execution time on amazon servers without time taken to transfer data in and out |
| originalRequest | object | Indicates parsed request from user |
| pointOfSale | string | Country ISO code where shopping request was generated. |
| destination | string | List of IATA codes indicating destination points, divided by comma |
| minDepartureDate | date | The earliest possible journey departure date |
| maxDepartureDate | date | The farthest possible journey departure date |
| minStay | number | Minimum number of days which should be spent at the point of destination before return journey |
| maxStay | number | Maximum mumber of days to be spent at the poing of destination before return journey |

Upon decompression of base64GzippedResponse and JSON data display the user should be able to view object contaning the following fields:

| Name | Example | Description |
| :--- | :--- | :--- |
| Destination | WAW | Destination code |
| Direct/Connected |  | Indicates whether proposal contains direct or connected flights |
| lastModified | 2017-03-20T12:25:02.943Z | Time in UTC format when data had been received from Travelport eStreaming |
| recordAgeInMs | 95917847 | Milliseconds passed from the moment, when data has been received |
| amount | 8820 | Pricing offer amount |
| currency | UAH | The currency of the PointofSale country. |
| validatingCarrier | PS | IATA code of plating carrier |
| originalRequest | 20171105IEVWAW20171110WAWIEV | Contains parsed request from user |
| Legs | 1 | Flight connection indicator |

#### Legs

This object contains the following parameters:

| Name | Example | Description |
| :--- | :--- | :--- |
| Origin | IEV | IATA code of airport/city where the journey begins |
| Destination | WAW | IATA code of airport/city where the journey ends |



