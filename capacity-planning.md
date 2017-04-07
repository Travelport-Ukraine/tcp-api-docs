# Capacity planning

We count simmultaneous concurrent transactions on RPS \(request per second\) basis. It is important to take into account both RPS limits and daily transaction limits \(for users subscribed to free tier\).

Free tier users might get  the following error messsage in case daily requests limit is exceeded

> { status: 'error',
>
>   dataAvailable: false,
>
>   requestId: '72a85761-19fb-11e7-a60b-c71e54dd7836',
>
>   executionTimeInMs: 184,
>
>   originalRequest: 
>
>    { pointOfSale: 'IT',
>
>      searchPhrase: '20170304CUFLCE',
>
>      minSearchDate: '2017-02-20',
>
>      maxSearchDate: '2017-02-26' },
>
>   errorMessage: 'Daily capacity limit exceeded' }

When the number of concurrent requests per second \(RPS\) is exceeded the relevant error message is also displayed.

> { status: 'error',
>
>   dataAvailable: false,
>
>   requestId: '72a85761-19fb-11e7-a60b-c71e54dd7836',
>
>   executionTimeInMs: 184,
>
>   originalRequest: 
>
>    { pointOfSale: 'IT',
>
>      searchPhrase: '20170304CUFLCE',
>
>      minSearchDate: '2017-02-20',
>
>      maxSearchDate: '2017-02-26' },
>
>   errorMessage: 'RPS capacity limit exceeded' }



