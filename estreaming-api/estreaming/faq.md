# FAQ

## 1. How long data is being kept in cache? <a id="1"></a>

Cache data is stored for 3 months from a day it was received, though it could be updated by _age of the data_. So you can see how long ago \(in milliseconds\) this data was processed on Travelport servers. Depending on your strategy and based on this figure your algorithm can decide if it can rely on this particular data set or it is outdated for your purposes.

## 2. Is cache data accuracy dependent on point of sale? <a id="2"></a>

Cache data accuracy depends on data volume and Travelport market share for a particular market.

## 3.When cached data is being refreshed? <a id="3"></a>

Cache data is being refreshed each time we receive search results from Travelport for a particular point of sale and search query.

Our data warehouse updates instantly with each incoming search result from Travelport. So practically data updates thousands time in a second to ensure that you'll always have an access to the most up to date and fresh information. Meanwhile, in all can see an age of each particular search result `recordAgeInMs` field. This field shows you a how many milliseconds passed from the moment, when data has been received from Travelport servers.

## 4. How many RPS eStreaming API could handle? <a id="4"></a>

eStreaming API is based on fully scalable architecture which allows us to process virtually unlimited RPS count.

## 5. Is it possible to search eStreaming API cache by cabin class? <a id="5"></a>

Because Business shopping is relatively rare, there is very low probability that it is possible to build respective cache on it. Data will always be outdated because of low frequency of host requests. Besides, business travelers are usually very demanding clients, and that is why majority of agencies uses direct requests to GDS to get the most sharp results for them. Fortunately there is not so many such requests and it should not seriously harm look 2 book ratio.

## 6. How to do requests for the same city pair, but in various points of sale? <a id="6"></a>

If you need to search the same route in different points of sale you would will need to make several requests to eSteaming API, so they would count as several requests. Depending on your programming strategy these requests could be sent simultaneously or consequently. eStreaming API supports both approaches.

## 7. We have 150 000 requests per day. Which RPS capacity do we need? <a id="7"></a>

Required RPS capacity is much dependent on the way how your requests are distributed during the day. Basic math shows that 150000 requests / 86400 seconds = 1.73 RPS per day.

But you should consider that requests distribution is not flat during the day. If, for example, you have almost no requests during the day and doubled activity during the night, you should reserve an amount of capacity that will be enough to serve your peak periods. However short bursts of activity should be taken into account, and it's highly recommended to implement consequent retry API calls in case you receive API response message, that you are over your capacity.

For further information about capacity, please visit [Capacity Planning](capacity-planning.md) page.

## 8. 1000 requests per day in a free tier is not enough for me. Can I ask you to give me more? <a id="8"></a>

We do not have 2000 or 10000 or any other than 1000 requests limits in free tier. The lowest possible daily limit after 1000 is 1 RPS. It is actually 86400 requests per day \(1 RPS \* 60 sec \* 60 min \* 24h\). It will cost you only 5 USD per day.

## 9. Which points of sale are available? <a id="9"></a>

Currently we process all data that Travelport sends us from following markets "AF", "AL", "AS", "BA", "BY", "CZ", "HR", "MD", "MK", "PL" , "RS", "SK", "SZ", "UA". Feel free to use any from this list in your requests. Historical data available for “CZ”, “PL”, “UA” markets for 3 months.

## 10. I need an additional point of sale which is not in the list. What should I do? <a id="10"></a>

We can process literally any number of point of sales that Travelport is ready to provide us with. However, our expenses are linearly dependent on the number of processed transactions. So there is no financial sense to process data from markets that do not have any clients yet. This is especially important for big markets. If you will express real interest to go for a paid access, we will be more than happy to turn on any additional markets.

## 11. Data about some particular route isn't available in selected point of sale? <a id="11"></a>

Please keep in mind, that some destinations are very unusual for some markets. For example PEK-LAX is very-very rare request for Ukranian agencies. Meanwhile, IEV-HRK is very rare in Australia. So the probability that someone ever searched this destination \(especially for some particular days of flights\) is infinitely low. For the test purposes, please use destinations that could be theoretically popular in appropriate market. Remember that any data that we have is a stat that someone searched before.

## 12. I've found a proposal that suits my customer's request. How can I book it? <a id="12"></a>

The best way to do a booking is [Travelport Universal API](https://www.travelport.com/solutions/travelport-universal-API). The sexiest way of using uAPI is [uAPI-JSON](https://github.com/Travelport-Ukraine/uapi-json). It depends on your booking strategy. But the best practice is the following:

Once you know Dates, Flight number, Fare, Airline etc, you can try to do a direct booking. If it is successful that's it. If seats are no longer available in this class, just send a direct booking request without fareBasisCode and bookingClass parameters as a result booking will be done in the cheapest available class on the same flight. It is strongly recommended to notify your client about price change if it is occurred.

## 13. Can I see my confidential \(negotiated\) fares in search results? <a id="13"></a>

Because of the obvious reasons Travelport doesn't share with us all confidential fares of all agencies from all over the World. However, we do consider an opportunity to build a private data partitions for some selected customers once this customer authorize us to process their confidential fares. It will require a separate processing and a separate data storage and as a result it will cause additional expenses for us. Currently we can discuss an opportunity of implementation of Private Data Partition only with clients who reserved 20+ RPS capacity for 3 month minimum.

## 14. I want to have a flat file with 1000 origin-destinations based on your data. Is it possible? <a id="14"></a>

Short answer: yes, you can build it on your side by calling methods of our API, but you'd better not do this.

A _flat files_ is an outdated approach which is still used by some data providers who are afraid or can not handle massive request form clients. This is why they are ready to answer you only twice a day \(or each hour\) with a big spreadsheet. The biggest issue with such files is they become outdated once you downloaded it. Even if you download updated flat file each hour during following 60 minutes we will receive more then 10 000 000 new search results and until you download a new version of file you'll be absolutely unaware of this updates. You'll get them only 60 minutes later. This approach seriously harms bookability because you'll be always trying to do a booking based on outdated information which means that some booking classes could be already unavailable.

But despite the above said, if you still want to build a flat file for 1000 O&D with 20 flight dates combinations for each O&D you can easily do it by sending us 20 000 [Cache API](https://docs.travelcloudpro.eu/cached-api.html) requests \(if you need all proposals for each request\) or 1000 [Fly From-To RT API](https://docs.travelcloudpro.eu/fly-from-to-api/fly-from-to-rt-api.html) requests \(if only cheapest direct & cheapest connected options is enough for you\). If you have for example 20 RPS \(Request per second\) capacity you can receive 1000 results in 1000/20 = 50 seconds, so about a minute would be enough for you to build such a file. When you need to update it you can repeat the whole process. You can execute this procedure however often you like. We are ready to process literally any number of simultaneous incoming request.

## 15. If I do not use flat files what is the best approach to use your API? <a id="15"></a>

Just consider that we already stored all available data on our servers for you and there is absolutely no practical sense to download some fraction of it on your site.

When someone comes to your web site and wants to know what are the most up-to-date pricing options from PAR to LON in 15th of Jan - just call [Cache API](https://www.gitbook.com/book/yulianagoncharenko/cee-esteaming-api/edit#) with appropriate parameters.

Once someone came to your web site and would like to take a look on a price calendar for NYC - MUC just call [Fly From-To RT API](https://www.gitbook.com/book/yulianagoncharenko/cee-esteaming-api/edit#) and you'll get necessary data in less then a second.

In both cases you'll get the latest data available for this point of time. In a contrast, if you'll be using any kind of flat files your data will be as old as your files are.

## 16. What should I do in order to increase bookability? <a id="16"></a>

Bookability is always a compromise between amount of expensive direct GDS requests and a number of cheap Cache results. Even none of GDS could guarantee you 100% bookability. While your clients are still looking at search results on your website some seats from this proposals could be sold by other agent on other side of the Earth. Consequently when you'll try to do a booking with this class you'll fail.

_Any_ cache solution will provide you with even lower bookability than GDS for an obvious reasons. Fortunately, we offer you a _global_ cache which updates not only by your requests, but by all request of all Travelport users globally.

However you can tune your cache bookability by cutting off some results extracted from cache. The best approach is the following:

1. Request data from [Cache API](https://www.gitbook.com/book/yulianagoncharenko/cee-esteaming-api/edit#)
2. Take a look to `recordAgeInMs` field in the results.  \(See answer \#3 of this FAQ\)
3. Take a look to how much time remains till the first flight
4. Based on this two figures you can do an assumption if data from the cache is reliable or not. If the first flight of the journey will be within 7 months and the age of this record in cache is 1 hour, it could be considered as very reliable because it is doubtful that something will be changed in availability of classes during an hour for the flight in such long future. On the contrary, if your first flight is tomorrow and you received data from the cache which was updated 5 days ago - this data is obviously outdated because classes availability for tomorrow's flights is changing each minute. 
5. If you consider data in the cache as unreliable just do a GDS Shopping request. Fortunately Cache check tooks just milliseconds any you would not depend too much time to do it. 
6. If cache data was as reliable just show it to your user as usual shopping result.

In our company we use following method to define reliability of cache result. Please feel free to use it in your projects. By changing `settings` you can tune how old data will be cut off.

```javascript
const settings = {
  defaultTtl: 3600,           // 1h
  baseTtl: 2592000,           // 30 days
  maxSearchPeriod: 31536000,  // 365 days
  multiplier: 3,              // maxTime = baseTtl * multiplier
  seed: 0.0001,               // 0.00001 <= seed <= 10000000 (smaller - bigger ttl values)
};

const getTTL = function getTTL(flightTime) {
  if (!flightTime) {
    return settings.defaultTtl;
  }

  const maxTtl = Math.round(settings.baseTtl / settings.multiplier);
  const now = (new Date()).getTime();
  const timeDiff = (flightTime instanceof Date)
    ? (flightTime.getTime() - now)/1000
    : (flightTime - now)/1000;

  if (timeDiff < 0) {
    return settings.defaultTtl;
  }

  return Math.round(
    settings.multiplier
    * (
      (maxTtl / Math.atan(settings.seed))
      * Math.atan(
        (
          (
            settings.multiplier
            * settings.seed
            * timeDiff
          ) / settings.maxSearchPeriod
        ) - settings.seed
      ) + maxTtl
    )
  );
};

module.exports = getTTL;

/**
 * Example
 * getTTL(new Date('2018-06-25'));
 */
```

## 17. I've tried to do a booking based on the cached or GDS results and it failed. What should I do next? <a id="17"></a>

Sometimes it happens when selected booking class is already gone \(see answer \#16 of this FAQ\). But it absolutely doesn't mean that we should loose this client. Most probably this plane is still full of the other available classes and you just should calmly explain to your client what happened and suggest other options. Internally in our company we use following approach:

1. Booking attempt has failed
2. Remember the price of proposal which you've been trying to book 
3. Call [.book\(params\)](https://github.com/Travelport-Ukraine/uapi-json/blob/master/docs/Air.md#bookparams) method of our free [uAPI JSON](https://github.com/Travelport-Ukraine/uapi-json) library _without_ `fareBasisCode` и `bookingClass` parameters but with mentioning all other flight details. 
4. [uAPI JSON](https://github.com/Travelport-Ukraine/uapi-json) will give you the cheapest available option on this particular flight straight from the GDS
5. Show an exclamation mark to a visitor with proposal to do a booking in a different class and ask if he/she agrees with following price change. 
6. If they agree, proceed with this booking
7. If they do not, just do a _new_ shopping request for the same O&D and dates and redirect this user there. 

If you do not use Node.JS / JavaScript in your project or if you are interested how [uAPI JSON](https://github.com/Travelport-Ukraine/uapi-json) does this trick you can take a look in [uAPI JSON](https://github.com/Travelport-Ukraine/uapi-json) source [code of .book method](https://github.com/Travelport-Ukraine/uapi-json/blob/master/src/Services/Air/Air.js#L32). Feel free to adopt this method in the language of your project and do not forget to share it as we did 😉

