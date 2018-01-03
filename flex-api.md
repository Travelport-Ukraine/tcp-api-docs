# Flex API

Provides ability to get the cheapest pricing option within pre-defined date range

## Flex API request

### Sample request \(type: GET\)

> [https://api.travelcloudpro.eu/v1/cache/flex?searchPhrase=20170501IEVWAW20170508WAWIEV&pointOfSale=UA](https://api.travelcloudpro.eu/v1/cache/flex?searchPhrase=20170501IEVWAW20170508WAWIEV&pointOfSale=UA)

### Request parameters:

| Name | Example | Description |
| :--- | :--- | :--- |
| searchPhrase | 20170501IEVWAW20170508WAWIEV | Departure and arrival date ranges whithin which cheapest options are received for a range dates before and/or after the requested flight date up to a maximum of three days. City IATA code required \(do not use airport code\). |
| pointOfSale | UA | Country ISO code where shopping request was generated. |

## Flex API response \(application/json\)

```js
"status": "success",
"dataAvailable": true,
"requestId": "e016a919-138c-11e7-b8a6-7fe3e3d1b344",
"executionTimeInMs": 150,
"originalRequest": {
    "searchPhrase": "20170501IEVWAW20170508WAWIEV",
    "pointOfSale": "UA"
},
"data": {
    "proposalsCount": 48,
    "compressedDataSize": 711,
    "uncompressedDataSize": 10390,
    "base64GzippedResponse": "H4sIAAAAAAAAA92aTWsbMRCG/4vOPqw0+szNSRNSKDjgtjmUHhZn2yy467LZFErwf6+aWxcmrWZmkZubvWuEHs3XOyN/elLfD/0wbb5s232nztSHtVqph64dd/c392P78PuZaXRorIlvLz/erm+fv7km5o/5Qf71m37sdpM6e1K7x3Hsht3P53Wu86vpMLX79bfD45DfK+2C9/npj3bf37VTP3y9aMex78b87t1GHVfq4jAMea3u7l9WszY5ZLXNVh2PKzJbKGezABrZzM22FC1EHbBzumaRuXIySB4jKzeaN2Ehm6VXazNPspmRs5lL2GLnhkOmGwJZSFgKKbeZt4B5I5NME8iseckbizaTuEFv8yJiDhQ0gNQxJ25oCJMlKxX0iR0aESUjpLOlbEYKDeewzZSTuXy4LzgAwxsJkki2uCYdl4kzgiCSJQtaTDakE5MNCbNZaQaBhhtnNtcKOZtpJ1Vc/yQj1TNJm3lwmAYp9cYZ2av1xvotlXFpGZsRsr6sN+YtLBJnFA0inUGWISPpRlGbmYA1i+fvi8hco/m6ERVEBDIdhZrFGVn9OIuAaX0mWfV6ZgCrZzwyktaPjZzW9zoIdTFzm1EySPLohKiiupqTVa/UAFjWL6zUc7Lq6goAc4BiMnNaGUQ3WAlZX7HI6lfqiMUZk4zSU4PBNkMgC+gonklGmYP8F2Skepa03J2X9xbTILwMUn3eKNfFzL2RkPWzzQQrtUfn+sU2A7YiNuhdDsFm3mJZn0lG0SAmCnYx3mDHxCSj1DMjeeVlUNcu7jzhpNSV9wnT+jyb0boYydwoqPWBn/UbzIEoWR+wqVwxmeUqYg/oLRPljw5yPbVle6PkpbkLRmj6PbcZRRFbLzlvRI+JR1ZdXbmQxDSI5dYz59DiSpqDLJRBSLpR8s5TsJ5Zdn8mSfY3b/z8C9mVHZ+WKAAA"
}
```

### Response parameters:

| Name | Data type | Description |
| :--- | :--- | :--- |
| status | string | Can be "success" or "error". Indicates an error while validating input params and while processing warehouse response. If the status is "error" then errorMessage is provided |
| dataAvailable | boolean | If value false is returned data is not avialable either because too distant dates indicated or some mandatory parameters not specified. In the latter case errorMessage is provided |
| requestId | string | Provides id for a API call |
| executionTimeInMs | number | Indicates execution time on amazon servers without time taken to transfer data in and out |
| originalRequest | object | Indicates parsed request from user |
| pointOfSale | string | Country ISO code where shopping request was generated. |
| data | response object | Appears only if status is "success" and dataAvailable is true |
| proposalsCount | number |  |
| compressedDataSize |  | compressed data size in bytes |
| uncompressedDataSize |  | uncompressed data size in bytes |
| base64GzippedResponse |  | gzipped response in base64 format |

Upon decompression of base64GzippedResponse and JSON data display the user should be able to view object contaning the following fields:

| Name | Example | Description |
| :--- | :--- | :--- |
| PointOfSale | UA | Destination code |
| searchPhrase | 20170428IEVWAW20170508WAWIEV | Indicates whether proposal contains direct or connected flights |
| Direct |  | Indicates that pricing option contains only direct flight |
| Connected |  | Shows that pricing option contains connecting flights |
| Currency | UAH | Pricing offer currency |
| TotalAmount | 15766 | Fare amount for the cheapest option, including taxes in PointofSale currency |
| ValidatingCarrier | LO | IATA code of the plating carrier |



