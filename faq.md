# Frequently asked questions

### 1. How long data is being kept in cache?

Cache data is stored for a year from a day it was received, though it could be updated by cheaper result \(in case of Historical cache\) or more fresh result \(in other cases\).

### 2. Is cache data accuracy dependent on point of sale?

Cache data accuracy depends on data volume for particular market.

### 3. When data in cache is being refreshed?

Cache data is being refreshed each time we receive search results from Travelport for particular point of sale and search query.

### 4. How many RPS eStreaming API could handle?

eStreaming API is based on fully scalable architecture which allows us to process virtually unlimited RPS count.

### 5. Is it possible to search eStreaming API cache by travel class?

Because Business shopping is relatively rare, there is very low probability that it is is possible to build respective cache on it. Data will always be outdated because of low frequency of host requests. Besides, business travelers are usually very demanding clients, and that is why majority of agencies uses direct requests to GDS to get the most sharp results for them. Fortunately there is not so much such requests and it should not seriously harm look 2 book ratio.

### 6. How do requests for the same city pair, but in various point of sales count?

If you need to search the same route in different point of sales would will need to make several requests to eSteaming API, and so they count as several requests.

### 7. We have 15000 requests per day. Which RPS capacity do we need?

Required RPS capacity is much dependent how your requests are distributed during the day. Basic math shows that 15000 requests / 86400 seconds = 1.73 RPS per day.

But you should consider that requests distribution is not flat during the day. If, for example, you have almost none requests during the night and doubled activity during the night, you should reserve an amount of capacity that will be enough to serve your peak periods. However short bursts of activity should be taken into account, and it's highly recommended to implement consequent retry API calls in case you receive API response message, that you are over your capacity.

For further information about capacity, please visit [Capacity Planning](/capacity-planning.md) page.

