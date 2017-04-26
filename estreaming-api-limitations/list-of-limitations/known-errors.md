### Cached API error response body example:

```
{
    "status": "error",
    "dataAvailable": false,
    "requestId": "10ec7a52-8c59-11e6-a503-532190b26d0f",
    "executionTimeInMs": 94,
    "originalRequest": {
        "searchPhrase": "20161012IEVWAW20161015WAWIEV",
        "pointOfSale": ""
    },
    "errorMessage": "No point of sale provided"
}
```

### Flex API error response body example \(application/json\):

```
{
    "status": "error",
    "dataAvailable": false,
    "requestId": "d4617c75-8c8b-11e6-a868-5d5f7099ab60",
    "executionTimeInMs": 257,
    "originalRequest": {
        "searchPhrase": "20181201IEVWAW20181205WAWIEV",
        "pointOfSale": ""
    },
    "errorMessage": "No point of sale provided"
}
```

### Flex API data is not available example:

```
{
    "status": "success",
    "dataAvailable": false,
    "requestId": "c613adda-8c8b-11e6-9b1c-6fc042573b18",
    "executionTimeInMs": 264,
    "originalRequest": {
        "searchPhrase": "20181201IEVWAW20181205WAWIEV",
        "pointOfSale": "UA"
    },
    "errorMessage": "No cache records found in warehouse"
}
```
