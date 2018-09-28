# Initiating request

Request URL  consists of the following elements depending on application method, API version

| Example | Description | Remark |
| :--- | :--- | :--- |
| [https://api.travelcloudpro.eu/v1/cache/shopping](https://api.travelcloudpro.eu/v1/cache/shopping) | Endpoint | includes API version |
| /cache | request type |  |
| /shopping | request name |  |
| ?searchPhrase | Departure and arrival dates and airport/city indicated in shopping request |  |
| &pointOfSale | Country ISO code where shopping request was generated. Further details can be found in [Point of Sale](https://www.gitbook.com/book/yulianagoncharenko/cee-esteaming-api/edit#/edit/master/pointofsale.md?_k=o5io60) Section |  |
| AuthToken | Available from Welcome letter with credentials | Indicated in  Postman Headers tab for each request |



