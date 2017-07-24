# Fly From-To API

Provides the cheapest pricing options for designated city/airport pair within specified time period and desirable minimum/maximum stay days.

## Fly From-To OW API request

### Sample request \(type: GET\)

> [https://api.travelcloudpro.eu/v1/cache/flyfromto?pointOfSale=UA&minDepartureDate=2017-10-01&maxDepartureDate=2017-10-07&origin=IEV&destination=WAW](https://api.travelcloudpro.eu/v1/cache/flyfromto?pointOfSale=UA&minDepartureDate=2017-10-01&maxDepartureDate=2017-10-07&origin=IEV&destination=WAW)

### Request parameters

The following table illustrates the minimum required data for From-To OW request.

| Name | Example | Desctiption |
| :--- | :--- | :--- |
| pointOfSale | UA | Country ISO code where shopping request was generated |
| minDepartureDate | 2017-11-01 | The earliest possible journey departure date |
| maxDepartureDate | 2017-11-07 | The farthest possible journey departure date |
| origin | IEV | City/airport IATA code where the journey begins |
| destination | WAW | City/airport IATA code where the journey ends |

## Fly From-To OW API response \(application/json\)

```js
{
    "status": "success",
    "dataAvailable": true,
    "requestId": "742461c6-0e3b-11e7-a5f2-a7bb8199509d",
    "executionTimeInMs": 62,
    "originalRequest": {
        "origin": "IEV",
        "destination": "WAW",
        "pointOfSale": "UA",
        "minDepartureDate": "2017-10-01",
        "maxDepartureDate": "2017-10-07",
        "minStay": null,
        "maxStay": null
    },
    "data": {
    "proposalsCount": 5,
    "compressedDataSize": 358,
    "uncompressedDataSize": 1703,
    "base64GzippedResponse": "H4sIAAAAAAAAA71UW0vDMBj9L3ley/flnrzVKThwbLDqQPGhtN1WqK2knSBj/91UfGzRDBnkKSeXc07OycuJvLdV0692m6wuiSWPCZmRrsxcflgfXNYNcxRQIQAu7p62ydbjt5Ur857YE8mPzpVN/vm9895DfdtndfLWHhuPEzSo/ORHVldF1lfNfp45V5XOQ+uNB+qs65dtUe2qsvi5KAIWUUhBWWosqFhK+exX+gtbVyT7ctEsO2IRNJdGCjjPyLxtGk9nOOFXQoyimCB0k/4PofMswFMW7inXyCYkPKymJGCEIgVtGbegYwQ1IkFIxlEaCibUVMWnGE2bGsgoyFV+QVKFmdIwnVQaoUkpWkb9+8eG6RENdBChJVM61FUuw6MayCjIVXG1/qNOQVpAP3zdRjVoKYSQPNxUJS/ofwihIE/VNf9Un4uhcCwWDMfaZhj4UIirfal/5XN+/QIDob/JpwYAAA=="
    }
}
```

### Response parameters

Please find below response elements for From-To OW API:

| Name | Data type | Description |
| :--- | :--- | :--- |
| status | string | Can be "success" or "error". Indicates an error while validating input params and while processing warehouse response. If the status is "error" then errorMessage is provided |
| dataAvailable | boolean | If value false is returned data is not avialable either because too distant dates indicated or some mandatory parameters not specified. In the latter case errorMessage is provided |
| requestId | string | Provides id for a API call |
| executionTimeInMs | number | Indicates execution time on amazon servers without time taken to transfer data in and out |
| originalRequest | object | Indicates parsed request from user |
| pointOfSale | string | Country ISO code where shopping request was generated. |
| searchPhrase | string | Departure and arrival dates and airport/city indicated in shopping request. The format is YYYYMMDDDEPARR, where DEP means Departure airport/city, ARR- arrival airport/city |
| minDepartureDate | date | Data format: YYYY-MM-DD. Marks the earliest date, staring from departure can take place |
| maxDepartureDate | date | Data format: YYYY-MM-DD. Indicates the last date, until which the flight should depart |
| minStay | null | No data for OW type of search |
| maxStay | null | No data for OW type of search |
| data | response object | Appears only if status is "success" and dataAvailable is true |
| proposalsCount | number | Indicates how many proposals are available in response |
| compressedDataSize |  | compressed data size in bytes |
| uncompressedDataSize |  | uncompressed data size in bytes |
| base64GzippedResponse |  | gzipped response in base64 formatUpon decompression of base64GzippedResponse and JSON data display the user should be able to view object contaning the following fields: |

Upon decompression of base64GzippedResponse and JSON data display the user should be able to view object contaning the following fields:

| Name | Data type | Description |
| :--- | :--- | :--- |
| pointOfSale | string | Country ISO code where shopping request was generated. |
| searchPhrase | string | Departure and arrival dates and airport/city indicated in shopping request. The format is YYYYMMDDDEPARR, where DEP means Departure airport/city, ARR- arrival airport/city |
| Direct | response object | Contains the cheapest prising option   for direct flight. Also contains gzippedshopping response in base64 format, to which this chepeast option referrs. For more information please see below |
| Connected | response object | Contains the cheapest option for connected flight. Also includes gzippedshopping response in base64 format, to which this chepeast option referrs. For more information please see below |

#### Direct pricing option object

| Name | Example | Description |
| :--- | :--- | :--- |
| currency | UAH | Pricing offer currency |
| totalAmount | 1913 | Fare amount for the cheapest option, including taxes in PointofSale currency |
| validatingCarrier | PS | IATA code of the plating carrier |
| lastModified | 2017-04-12T17:37:44.098Z | Time in UTC format when data had been received from Travelport eStreaming |
| recordAgeInMs | 55591865 | Milliseconds passed from the moment, when data has been received |

#### Connected pricing option object

| Name | Example | Description |
| :--- | :--- | :--- |
| currency | UAH | Pricing offer currency |
| totalAmount | 3732 | Fare amount for the cheapest option, including taxes in PointofSale currency |
| validatingCarrier | BT | IATA code of the plating carrier |
| lastModified | 2017-04-12T17:37:44.098Z | Time in UTC format when data had been received from Travelport eStreaming |
| recordAgeInMs | 55591865 | Milliseconds passed from the moment, when data has been received |

## 



