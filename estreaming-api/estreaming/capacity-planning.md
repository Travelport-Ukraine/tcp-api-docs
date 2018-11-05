# Capacity Planning

eStreaming API pricing is based on RPS \(requests per seconds\).

Our free tier is a subject of **daily transactions limit** and **1RPS** capacity limitation.

If you want to use eStreaming API without this limitations, you have to calculate the capacity you need, and then reserve it for you.

## Reserved capacity calculation

We recommend following approach for the capacity calculation.

1. End user of API studies log log files of his web site.
2. After log files analysis, assumptions and estimations are made on how many concurrent requests per second will be send to eStreaming API.
3. Calculated number of concurrent requests is called reserved capacity.

## Ordering and changing reserved capacity

After you order your reserved capacity your daily transactions limit will be removed and you'll able to run queries according to selected RPS capacity.

You can feel free to change your reserved capacity by one day advance notice.

## Handling request bursts on your site

It is highly possible you are going to experience short periodic bursts of requests activity on your site. We recommend you to implement consequent retry API calls in case you receive API response message, that you are over your capacity.

If you are running into bursts too frequently, we recommend you to increase you reserved capacity.

## Capacity error messages

Free tier users might get the following error message in case daily requests limit is exceeded

```javascript
 {
     status: 'error',
     dataAvailable: false,
     requestId: '72a85761-19fb-11e7-a60b-c71e54dd7836',
     executionTimeInMs: 184,
     originalRequest: {
         pointOfSale: 'IT',
         searchPhrase: '20170304CUFLCE',
         minSearchDate: '2017-02-20',
         maxSearchDate: '2017-02-26'
     },
     errorMessage: 'Daily capacity limit exceeded'
 }
```

When the number of concurrent requests per second \(RPS\) is exceeded the relevant error message is also displayed.

```javascript
{
    status: 'error',
    dataAvailable: false,
    requestId: '72a85761-19fb-11e7-a60b-c71e54dd7836',
    executionTimeInMs: 184,
    originalRequest: {
        pointOfSale: 'IT',
        searchPhrase: '20170304CUFLCE',
        minSearchDate: '2017-02-20',
        maxSearchDate: '2017-02-26'
    },
    errorMessage: 'RPS capacity limit exceeded'
}
```

