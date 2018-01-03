# **Historical API**

Provides shopping results based on general shopping request within designated time period from specific point \(s\) of sale. Allows to analyze prise fluctuations, off- peak and price jumps for specific destinations

## Historical API request

### Sample request \(type: GET\)

> [https://api.travelcloudpro.eu/v1/cache/history?searchPhrase=20170522IEVWAW&pointOfSale=UA&minSearchDate=2017-01-03&maxSearchDate=2017-01-10](https://api.travelcloudpro.eu/v1/cache/history?searchPhrase=20170522IEVWAW&pointOfSale=UA&minSearchDate=2017-01-03&maxSearchDate=2017-01-10)

### Request parameters

The following table illustrates the minimum required data for cached shopping request.

| Name | Example | Description |
| :--- | :--- | :--- |
| searchPhrase | 20170522IEVWAW | Departure and arrival dates and city codes indicated in shopping request. The format is YYYYMMDDDEPARR, where DEP means Departure city, ARR- arrival city code \(do not use airport code\) |
| pointOfSale | UA | Country ISO code where shopping request was generated |
| minSearchDate | 2017-01-03 | Departure date marking the beginningof search results streaming |
| maxSearchDate | 2017-01-10 | Departure date marking the end of search results streaming |

## Historical API response

### Response example \(application/json\)

```js
{
    "status": "success",
    "dataAvailable": true,
    "requestId": "42880234-0a5f-11e7-89f3-6b9a48544cdd",
    "executionTimeInMs": 244,
    "originalRequest": {
        "pointOfSale": "UA",
        "searchPhrase": "20170522IEVWAW",
        "minSearchDate": "2017-01-03",
        "maxSearchDate": "2017-01-10"
    },
    "data": {
        "proposalsCount": 1,
        "compressedDataSize": 2914,
        "uncompressedDataSize": 7341,
        "base64GzippedResponse": "H4sIAAAAAAAAA+2Xx67EyG6G3+VsNWPlNDvlnLMMw1ArZ7Wy+uK+u3suYK8MeG8cLUmCJdZfRdb37/...
    }
}
```

| Name | Data type | Description |
| :--- | :--- | :--- |
| status | string | Can be "success" or "error". Indicates an error while validating input params and while processing warehouse response. If the status is "error" then errorMessage is provided |
| dataAvailable | boolean | If value false is returned data is not available either because too distant dates indicated or some mandatory parameters not specified. In the latter |
| requestId | string | Provides id for an API call |
| executionTimeInMs | number | Indicates execution time on Amazon servers without time taken to transfer data in and out |
| originalRequest | object | Indicates parsed request from user |
| pointOfSale | string | Country ISO code where shopping request was generated. |
| searchPhrase | string | Departure and arrival dates and city codes indicated in shopping request. The format is YYYYMMDDDEPARR, where DEP means Departure city, ARR- arrival city code \(do not use airport code\) |
| minSearchDate | date | Data format: YYYY-MM-DD. Marks the earliest date, starting from which search results are streamed |
| maxSearchDate | date | Data format: YYYY-MM-DD. Indicates the last date, until which search results are streamed |
| data | response object | Appears only if status is "success" and dataAvailable is true |
| proposalsCount | number | Indicates how many proposals are available in response |
| compressedDataSize |  | compressed data size in bytes |
| uncompressedDataSize |  | uncompressed data size in bytes |
| base64GzippedResponse |  | gzipped response in base64 format |

Upon decompression of base64GzippedResponse and JSON data display the user should be able to view object containing the following fields:

| Name | Data type | Description |
| :--- | :--- | :--- |
| pointOfSale | string | Country ISO code where shopping request was generated. |
| searchPhrase | string | Departure and arrival dates and city codes indicated in shopping request. Original shopping query, containing departure and arrival dates and city indicated in shopping request. The format is YYYYMMDDDEPARR, where DEP means Departure city/airport code ARR- arrival city/airport code  |
| searchDate | date | Date in the format YYYY-MM-DD to which the search results refer |
| Direct | response object | Contains the cheapest pricing option   for direct flight. Also contains gzippedshopping response in base64 format, to which this cheapest option |
| Connected | response object | Contains the cheapest option for connected flight. Also includes gzipped shopping response in base64 format, to which this chepeast option refers. For more information please see below |

### Direct

| Name | Data type | Description |
| :--- | :--- | :--- |
| currency | string | The currency of the PointofSale country. |
| totalAmount | number | Fare amount for the cheapest option, including taxes in PointofSale currency |
| validatingCarrier | string | IATA code of the plating carrier |
| warehouseId |  | Unique identifier of the particular data in the warehouse \(this field changes when new data on the same request is received, while data is still available using warehouseId\) |
| dataSizeInBytes |  | Size of the compressed data |
| base64GzippedResponse |  | Shopping response in which the cheapeast direct offer to this search request was found, gzipped response in base64 format |

Shopping reponse contains the following elements:

* Headers
* Date
* Proposals

#### Header

| Name | Example | Description |
| :--- | :--- | :--- |
| guid | 46de111d-180a-4094-b4bf-4aa435e20b33 | Unique id |
| requestStart | 2017/03/11 18:22:02.525 |  |
| pointOfSale | UA | Country ISO code where shopping request was generated. |
| originalRequest | 20170316IEVWAW20170319WAWIEV | Original shopping query, containing departure and arrival dates and city indicated in shopping request.The format is YYYYMMDDDEPARR, where DEP means Departure city/airport code ARR- arrival city/airport code. |

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

| Name | Example | Description |
| :--- | :--- | :--- |
| FareBasisCode | UUATBAS | The Fare Basic Code \(FBC\) for this fare |
| FareType | XPN | Fare type |
| TechnicalStops | 0 | Count of Incidental Stops |
| Duration | 00130 | Flight duration, in the format Dhhmm |
| Origin | PRG | Origin of travel |
| Destination | WAW | Destination point |
| DepartureTime | 201705220705 | Departure date/time in the format \(YYYYMMDDhhmm\) |
| ArrivalTime | 201705220835 | Arrival date/time in the format YYYYMMDDhhmm |
| OutTerminal | 2 | Departure terminal |
| InTerminal | 1 | Arrival terminal |
| MarketingCarrier | OK | Marketing carrier of Flight |
| OperatingCarrier | OK | Operating Carrier of Flight |
| FlightNumber | 0782 | Flight number for each leg |
| BookingCode | W | Booking code for each leg |
| Cabin | E | Cabin for each leg |
| Seats | 001 | Seats for each leg |
| AvailabilitySource | B | Where availability was obtained |
| Equipment | E75 | Equipment type |
| SegmentsContinued | 1M | Indicates married segments |



