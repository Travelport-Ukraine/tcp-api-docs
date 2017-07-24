# Fly From API

Contains the cheapest pricing options for all flights operated from defined city or airport on desirable dates.

## Fly From API request

### Sample request \(type: GET\)

> [https://api.travelcloudpro.eu/v1/cache/flyfrom?origin=IEV&pointOfSale=UA](https://api.travelcloudpro.eu/v1/cache/flyfrom?origin=IEV&pointOfSale=UA)

### Request parameters

The following table illustrates the minimum required data for Fly From API request.

| Name | Example | Description |
| :--- | :--- | :--- |
| origin | IEV | City/airport IATA code from which journey begins |
| pointOfSale | UA | Country ISO code where shopping request was generated. Maximum one point of sale is allowed per each request. |

## Fly From API response

### Response sample \(application/json\)

```js
{
    "status": "success",
    "dataAvailable": true,
    "requestId": "912cd26f-0e47-11e7-af3f-8d3df4e11839",
    "executionTimeInMs": 1340,
    "originalRequest": {
        "origin": "IEV",
        "pointOfSale": "UA"
    },
    "data": {
        "proposalsCount": 1397,
        "compressedDataSize": 75493,
        "base64GzippedResponse": "H4sIAAAAAAAAA6y9a48muY0u+F/683RA1F31rTKz7lmZ1Xmp25cDY8Y7MDDrwXpmFlgcnP++pKSIUBh8lWR12Iah6La7KL0UxcvDh/...
    }
}
```

### Response parameters

Please find below response elements for FlyFrom API:

| Name | Data type | Description |
| :--- | :--- | :--- |
| status | string | Can be "success" or "error". Indicates an error while validating input params and while processing warehouse response. If the status is "error" then errorMessage is provided |
| dataAvailable | boolean | If value false is returned data is not avialable either because too distant dates indicated or some mandatory parameters not specified. In the latter case errorMessage is provided |
| requestId | string | Provides id for a API call |
| executionTimeInMs | number | Indicates execution time on amazon servers without time taken to transfer data in and out |
| originalRequest | object | Indicates parsed request from user |
| pointOfSale | string | Country ISO code where shopping request was generated. |
| data | response object | Appears only if status is "success" and dataAvailable is true |
| proposalsCount | number | Indicates how many proposals are available in response |
| compressedDataSize |  | compressed data size in bytes |
| uncompressedDataSize |  | uncompressed data size in bytes |
| base64GzippedResponse |  | gzipped response in base64 formatUpon decompression of base64GzippedResponse and JSON data display the user should be able to view object contaning the following fields: |

Upon decompression of base64GzippedResponse and JSON data display the user should be able to view object contaning the following fields:

| Name | Example | Description |
| :--- | :--- | :--- |
|  | AAE | Destination code |
| RT\_Connected/Direct, OW\_Direct/Connected |  | Indicates whether proposals referrs to RT or OW journey, containing direct or connected flights |
| lastModified | 2017-03-20T12:25:02.943Z | Time in UTC format when data had been received from Travelport eStreaming |
| recordAgeInMs | 95917847 | Milliseconds passed from the moment, when data has been received |
| amount | 8820 | Pricing offer amount |
| currency | UAH | The currency of the PointofSale country. |
| validatingCarrier | PS | IATA code of plating carrier |
| originalRequest | 20170501IEVAAL20170521AALIEV | Contains parsed request from user |



