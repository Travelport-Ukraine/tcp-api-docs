# Fly From To RT API

One \(single\) request allows to extract data with total length of departure dates range + stay days range up to 20.

## Sample request

> [https://api.travelcloudpro.eu/v1/cache/flyfromto?pointOfSale=UA&minDepartureDate=2017-11-01&maxDepartureDate=2017-11-07&origin=IEV&destination=AMS&minStay=2&maxStay=5](https://api.travelcloudpro.eu/v1/cache/flyfromto?pointOfSale=UA&minDepartureDate=2017-11-01&maxDepartureDate=2017-11-07&origin=IEV&destination=AMS&minStay=2&maxStay=5)

The following table shows minimum parameters for FlyFromTo RT request.

| Name | Example | Description |
| :--- | :--- | :--- |
| pointOfSale | UA | Country ISO code where shopping request was generated |
| minDepartureDate | 2017-11-01 | The earliest possible journey departure date |
| maxDepartureDate | 2017-11-07 | The farthest possible journey departure date |
| origin | IEV | City/airport IATA code from which journey begins |
| destination | AMS | City/airport IATA code where the journey ends |
| minStay | 2 | Minimum number of days which should be spent at the point of destination before return journey |
| maxStay | 5 | Maximum mumber of days to be soent at the poing of destination before return journey |

## Sample response \(application/json\)

```javascript
{
    "status": "success",
    "dataAvailable": true,
    "requestId": "c0b8fc4c-0e3a-11e7-ba5b-d5670f74ff75",
    "executionTimeInMs": 103,
    "originalRequest": {
        "origin": "IEV",
        "destination": "AMS",
        "pointOfSale": "UA",
        "minDepartureDate": "2017-11-01",
        "maxDepartureDate": "2017-11-07",
        "minStay": "2",
        "maxStay": "5"
    },
    "data": {
        "proposalsCount": 8,
        "compressedDataSize": 493,
        "uncompressedDataSize": 2831,
        "base64GzippedResponse": "H4sIAAAAAAAAA72WTWvbQBCG/8ueHbEzs6P9uKlpS0NjHLDbQ0sPwlYSgSsVWSmU4P/eUcmhBa2dlUVBB2ln2X3n0cy7+/VZ/Wjrpl/dr8t9pYL6VKiFOlRlt328e+zKwzCGGiyAhpt3n4vl+uWL5VUGZPbbuqu2vQrPavvUdVWz/fVnnQ8S6tu+3Bff26dG4sp5rWXwZ7mvd2VfNw/XZdfVVSehu7UE9uWhX7a7+r6udi/bXmm6Ar9BHbQPhjO25ovMlA3bblc8VDfN8qACGOdJW+uOC3XdNo3IGVY4KyhngIig29U8go6LBML4D+F8AmGHZgph3gAFY4NxmUUYSYjBGmNzgkTC7MBHBL3ZzCPoAsL2vxI2AVkqI/O5HU2IZTI5TiUsdRYRVLyfR9AFhM0Ul6CYS3y8PZ2QC8NDmSMeS0gDIkrhzOcSqzO//LWCLiA8xYedneTDdmhKdIEgc4gjCZFhp41UZCphMm6KSyQISiJMMxCONeUpwggbnQdDQbtMWz+SEBpGh5aSS5hoQgkn6LmA7wQX9ogxvmc8Yji1rfhe5owba0kCaQ7WJtWFmWMtdeace7WgJML2b8IAU1wYYxVzkrAdEiIfgDOtx65GxJ5zkIZPJYw+5hEnz7kEQcdvvwHYvqO6DwsAAA=="
    }
}
```

Please find below the description of From-To RT elements:

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
| minStay | number | Minimum number of days which should be spent at the point of destination before return journey |
| maxStay | number | Maximum number of days which should be spent at the point of destination before return journey |
| data | response object | Appears only if status is "success" and dataAvailable is true |
| proposalsCount | number | Indicates how many shopping proposals are available in response |
| compressedDataSize |  | compressed data size in bytes |
| uncompressedDataSize |  | uncompressed data size in bytes |
| base64GzippedResponse |  | gzipped response in base64 format |

Upon decompression of base64GzippedResponse and JSON data display the user should be able to view object contaning the following fields:

| Name | Data type | Description |
| :--- | :--- | :--- |
| pointOfSale | string | Country ISO code where shopping request was generated. |
| searchPhrase | string | Departure and arrival dates and airport/city indicated in shopping request. The format is YYYYMMDDDEPARR, where DEP means Departure airport/city, ARR- arrival airport/city |
| Direct | response object | Contains the cheapest prising option   for direct flight. Also contains gzippedshopping response in base64 format, to which this chepeast option referrs. For more information please see below |
| Connected | response object | Contains the cheapest option for connected flight. Also includes gzippedshopping response in base64 format, to which this chepeast option referrs. For more information please see below |

### Direct pricing option object

| Name | Example | Description |
| :--- | :--- | :--- |
| currency | UAH | Pricing offer currency |
| totalAmount | 1913 | Fare amount for the cheapest option, including taxes in PointofSale currency |
| validatingCarrier | PS | IATA code of the plating carrier |
| lastModified | 2017-04-12T17:37:44.098Z | Time in UTC format when data had been received from Travelport eStreaming |
| recordAgeInMs | 55591865 | Milliseconds passed from the moment, when data has been received |

### Connected pricing option object

| Name | Example | Description |
| :--- | :--- | :--- |
| currency | UAH | Pricing offer currency |
| totalAmount | 3732 | Fare amount for the cheapest option, including taxes in PointofSale currency |
| validatingCarrier | BT | IATA code of the plating carrier |
| lastModified | 2017-04-12T17:37:44.098Z | Time in UTC format when data had been received from Travelport eStreaming |
| recordAgeInMs | 55591865 | Milliseconds passed from the moment, when data has been received |

