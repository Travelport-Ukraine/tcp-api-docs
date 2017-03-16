# **Historical API**

Provides shopping results based on general shopping request within designated time period from specific point \(s\) of sale. Allows to analyze prise fluctuations, off- peak and price jumps for specific destinations

## Historical API request

| Name | Example | Description |
| :--- | :--- | :--- |
| searchPhrase | 20171022IEVTLV | Departure and arrival dates and airport/city indicated in shopping request. The format is YYYYMMDDDEPARR, where DEP means Departure airport/city, ARR- arrival airport/city |
| pointOfSale | UA | Country ISO code where shopping request was generated |
| minSearchDate | 2017-08-25 | Departure date marking the beginningof search results streaming |
| maxSearchDate | 2016-08-30 | Departure date marking the end of search serults streaming |

## Historical API response

### Response example

> {
>
> "status": "success",
>
> "dataAvailable": true,
>
> "requestId": "42880234-0a5f-11e7-89f3-6b9a48544cdd",
>
> "executionTimeInMs": 244,
>
> "originalRequest": {
>
> ```
> "pointOfSale": "UA",
>
> "searchPhrase": "20170522IEVWAW",
>
> "minSearchDate": "2017-01-03",
>
> "maxSearchDate": "2017-01-10"
> ```
>
> },
>
> "data": {
>
> ```
> "proposalsCount": 1,
>
> "compressedDataSize": 2914,
>
> "uncompressedDataSize": 7341,
>
> "base64GzippedResponse": "H4sIAAAAAAAAA+2Xx67EyG6G3+VsNWPlNDvlnLMMw1ArZ7Wy+uK+u3suYK8MeG8cLUmCJdZfRdb37/....
> ```

| Name | Data type | Description |
| :--- | :--- | :--- |
|  |  |  |



