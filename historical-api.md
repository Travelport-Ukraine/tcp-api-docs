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
| status | string | Can be "success" or "error". Indicates an error while validating input params and while processing warehouse response. If the status is "error" then errorMessage is provided |
| dataAvailable | boolean | If value false is returned data is not avialable either because too distant dates indicated or some mandatory parameters not specified. In the latter case errorMessage is provided |
| requestId | string | Provides id for a API call |
| executionTimeInMs | number | Indicates execution time on amazon servers without time taken to transfer data in and out |
| originalRequest | object | Indicates parsed request from user |
| pointOfSale | string | Country ISO code where shopping request was generated. |
| searchPhrase | string | Departure and arrival dates and airport/city indicated in shopping request. The format is YYYYMMDDDEPARR, where DEP means Departure airport/city, ARR- arrival airport/city |
| minSearchDate | date | Data format: YYYY-MM-DD. Marks the earliest date, staring from which search results are streamed |
| maxSearchDate | date | Data format: YYYY-MM-DD. Indicates the last date, until which search results are streamed |
| data | response object | Appears only if status is "success" and dataAvailable is true |
| proposalsCount | number | Indicates how many proposals are available in response |
| compressedDataSize |  | compressed data size in bytes |
| uncompressedDataSize |  | uncompressed data size in bytes |
| base64GzippedResponse |  | gzipped response in base64 format |

Upon decompression of base64GzippedResponse and JSON data display the user should be able to view object contaning the following fields:

| Name | Data type | Description |
| :--- | :--- | :--- |
| pointOfSale | string | Country ISO code where shopping request was generated. |
| searchPhrase | string | Departure and arrival dates and airport/city indicated in shopping request. The format is YYYYMMDDDEPARR, where DEP means Departure airport/city, ARR- arrival airport/city |
| searchDate | date | Date in the format YYYY-MM-DD to which the search results refer |
| Direct | response object | Contains the cheapest prising option   for direct flight. Also contains gzippedshopping response in base64 format, to which this chepeast option referrs. For more information please see below |
| Connected | response object | Contains the cheapest option for connected flight. Also includes gzippedshopping response in base64 format, to which this chepeast option referrs. For more information please see below |

### Direct

| Name | Data type | Description |
| :--- | :--- | :--- |
| currency | string | The currency of the PointofSale country. |
| totalAmount | number | Fare amount for the cheapest option, including taxes in PointofSale currency |
| validatingCarrier | string | IATA code of the plating carrier |
| warehouseId |  | Unique identifier of the particular data in the warehouse \(this field changes when new data on the same request is received, while data is still available using warehouseId\) |
| dataSizeInBytes |  | Size of the compressed data |
| base64GzippedResponse |  | Shopping response in which the chepeast direct offer to this search request was found, gzipped response in base64 format |

Shopping reponse contains the following elements:

* Headers
* Date
* Proposals

#### Header

| Name | Example | Description |
| :--- | :--- | :--- |
| guid | 46de111d-180a-4094-b4bf-4aa435e20b33 | Unique id |
| requestStart | 2017/03/11 18:22:02.525 | ? |
| pointOfSale | UA | Country ISO code where shopping request was generated. |
| originalRequest | 20170316IEVWAW20170319WAWIEV | Original shopping query, containing departure and arrival dates and airport/city indicated in shopping request. The format is YYYYMMDDDEPARR, where DEP means Departure airport/city, ARR- arrival airport/city |

#### Date

Date and time when data was transmitted to eStreaming API server.

#### Proposal

Each proposal represents shopping results containing a number of pricing options. A pricing option contains the following elements

| Name | Data type | Description |
| :--- | :--- | :--- |
| Currency | string | The currency of the PointofSale country. |
| TotalFareAmount | number | Fare amount including taxes in PointofSale currency |
| Taxes | number | Tax amount in PointofSale currency |
| Validating Carrier | string | IATA code of the validating vendor |
| Legs | number | See more detailed Leg description below |

#### Leg

A leg is basically a part of journey between two cities/airports, that can contain one segment in case of direct flights or multiple flight segments in case of connection or stopover.

| Name | Data type | Desctiption |
| :--- | :--- | :--- |
| PassengerTypeCode | string | IATA Passenger Type Code \(PTC\) that normally contains 3 letters: ADT, SRC, CNN etc |
| Segments | number | Quantity of segments within one leg. See more details below |

##### Segments

| Name |  |  |
| :--- | :--- | :--- |
| FareBasisCode |  | The Fare Basic Code \(FBC\) for this fare |
| FareType |  | Fare type |
| TechnicalStops |  |  |
| Duration |  |  |
| Origin |  |  |
| Destination |  |  |
| DepartureTime |  |  |
| ArrivalTime |  |  |
| OutTerminal |  |  |
| InTerminal |  |  |
| MarketingCarrier |  |  |
| OperatingCarrier |  |  |
| FlightNumber |  |  |
| BookingCode |  |  |
| Cabin |  |  |
| Seats |  |  |
| AvailabilitySource |  |  |
| Equipment |  |  |
| SegmentsContinued |  |  |





