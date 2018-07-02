---
description: This page describes how to make a request against TCP eStreaming API
---

# Making request

To run a request against TCP eStreaming API you should make a proper GET request against on of the API methods, providing all required params.

## Authorization

To authorize you against the API we use `AuthToken` header, which should be passed with each and every request. You always receive one, when you register in TCP.

## Request URL

Typical request URL looks like that:

> [https://api.travelcloudpro.eu/v1/cache/shopping?searchPhrase=20181009IEVIST20181015ISTIEV&pointOfSale=UA&ptc=ADT](https://api.travelcloudpro.eu/v1/cache/shopping?searchPhrase=20181009IEVIST20181015ISTIEV&pointOfSale=UA&ptc=ADT)

Request URL consists of the following elements:

| **URL part** | **Description** |
| :--- | :--- | :--- |
| [https://api.travelcloudpro.eu](https://api.travelcloudpro.eu) | API endpoint |
| /v1 | API version |
| /cache | API application \(cache stands here for eStreaming API\) |
| /shopping | API method |
| ?searchPhrase=...&... | API query params |

## Common required params

Common eStreaming API request has following required params:

| **Query param name** | **Description** |
| --- | --- | --- |
| pointOfSale | Country ISO code where shopping request was generated. Further details can be found in [Point of Sale](point-of-sale.md) Section. |
| ptc | Comma separated list of PTC \(e.g "ADT,CNN", "ADT" or "ITX"\) |

