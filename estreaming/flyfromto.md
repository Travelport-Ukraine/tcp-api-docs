# Fly From-To API

Provides the cheapest pricing options for designated city/airport pair witihin specified time period and desirable minimum/maximum stay days.

## Fly From-To API request

| Name | Example | Description |
| :--- | :--- | :--- |
| pointOfSale | UA | Country ISO code where shopping request was generated. Maximum one point of sale is allowed per each request. |
| minDepartureDate | 2017-10-01 | The earliest possible journey departure date |
| maxDepartureDate | 2017-10-07 | The farthest possible journey departure date |
| origin | IEV | City/airport IATA code from which journey begins |
| destination | WAW | City/airport IATA code where the journey ends |
| minStay | 2 | Minimum number of days which should be spent at the point of destionationbefore return journey begins |
| maxStay | 5 | Maximum mumber of days to be soent at the poing of destination before return journey begins |

## Fly From-To API response



