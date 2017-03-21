# Cache API

Allows to aggregate shopping results and build pricing database based on general shopping query with point of sale included.

## Cache API request

### Example

> [https://api.travelcloudpro.eu/v1/cache/shopping?searchPhrase=20170316IEVWAW20170319WAWIEV&pointOfSale=UA](https://api.travelcloudpro.eu/v1/cache/shopping?searchPhrase=20170316IEVWAW20170319WAWIEV&pointOfSale=UA)

### Request parameters

The following table illustrates the minimum required data for cached shopping request.

| Name | Example | Description |
| :--- | :--- | :--- |
| searchPhrase | 20171012IEVWAW20171015WAWIEV | Departure and arrival dates and airport/city indicated in shopping request. The format is YYYYMMDDDEPARR, where DEP means Departure airport/city, ARR- arrival airport/city |
| pointOfSale | UA | Country ISO code where shopping request was generated. |

## Cache API response

### Response example

> {
>
> "status": "success",
>
> "dataAvailable": true,
>
> "requestId": "f0338277-07d7-11e7-8d76-93c818f06757",
>
> "executionTimeInMs": 328,
>
> "originalRequest": {
>
> ```
> "searchPhrase": "20170316IEVWAW20170319WAWIEV",
>
> "pointOfSale": "UA"
> ```
>
> },
>
> "data": {
>
> ```
> "lastModified": "2017-03-11T18:22:02.525Z",
>
> "recordAgeInMs": 144447048,
>
> "dataSizeInBytes": 17578,
>
> "warehouseId": "main\_data/2017/03/11/18/bd1a1bc2-88bf-40be-989e-f5fd25bf1ab2.gz:100533:17578",
> ```
>
> "base64GzippedResponse": "H4sIAAAAAAAAA+2dXZPcNpKu78+vOKHr8Vl8kAA5d9Ufsjq61ZKqqiVbJ.........

| Name | Data type | Description |
| :--- | :--- | :--- |
| status | string | Can be "success" or "error". if status is "success" indicates if the data exists in the warehouse. indicates an error while validating input params and while processing warehouse response. |
| dataAvailable | boolean | If value false is returned data is not avialable either because too distant dates indicated or some mandatory parameters not specified. In the latter case errorMessage is provided |
| requestId | string | Provides id for a API call |
| executionTimeInMs | number | Indicates execution time on amazon servers without time taken to transfer data in and out |
| originalRequest | object | Contains parsed request from user |
| errorMessage | string | Appears if status is "error" or if dataAvailable is false. See Known issues for more detailed information about most frequestnly returned errors. |
| data | response object | Is shown when status is "success" anddataAvailable is true |
| lastModified |  | Time in UTC format when data had been received from Travelport eStreaming |
| recordAgeInMs |  | Milliseconds passed from the moment, when data has been received |
| dataSizeInBytes |  | Size of the compressed data |
| warehouseId |  | Unique identifier of the particular data in the warehouse \(this field changes when new data on the same request is received, while data is still available using warehouseId\) |
| base64GzippedResponse |  | gzipped response in base64 format |

Upon decompression of base64GzippedResponse and JSON data display the user should be able to view object contaning 3 items:

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
| Legs | number | Flight connection indicator |

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



