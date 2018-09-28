# Exchange API

We did our best to create the simpliest solution for exchanging tickets, yet coming with all powerful and elastic features, you can expect from the Travel Cloud Pro.

## Authorization and authentication

In order to execute Exchange API methods you need to authenticate to obtain `AuthToken`. Then you will need to pass `AuthToken` header with each request to authorize it.

For information on how to obtain `AuthToken` see [Authorization and authentication](exchange-api/exchange/authorization.md) article.

## PCC switching

If you have more than one PCC in your TCP account, you may find useful switching your PCCs with [ChangePcc](exchange-api/exchange/change-pcc.md) method.

## Exchange procedure

### 1. Select a PNR to start with

Exchange starts with PNR. You need to have one before proceeding. If you are going to do a name change, or your previous PNR is now archived, you are to create a new one. In order to check if you have chosen the right one, use our [GetBooking](exchange-api/methods/get-booking.md) method.


### 2. Add segments to PNR

Exchanges are always connected with the change of segments data. You would have two options to deal with new segments.

* Add new segments to the PNR by yourself and save it
* Proceed without adding new segments, passing new segments information in appropriate format into next steps when it's required

### 3. Get a quote

If you want to get a quote with your new segments, which are not yet added to PNR, pass them along with the current PNR segments, having the attribute `isSaved` set to `false`.

You can get a quote by running [CalculateExchangeInformation](./exchange/calculate-exchange-information.md) method by passing there your PNR, number of the ticket you're going to exchange and segments you have chosen, including informative segments. Fare quote will not be saved at the moment.

If you have already created fare quote on your side, you may still run [CalculateExchangeInformation](./exchange/calculate-exchange-information.md) providing an index of your fare quote.

### 4. Process an exchange

You have to use [ExchangeTicket](./exchange/exchange-ticket.md) method in order to process an exchange. We will need some data from your side in order to continue.

* PNR
* Ticket Number
* Fare quote index OR Fare quote data (used on a previous step to get a quote)
* Exchange data
  * Commission
  * Expected ADC and refund values
  * Penalty information
  * IT/BT flags, tour code, endorsement and other updates to fare quote (optional)
  * Form of payment (if applicable)
* Copy options (if several passengers are to be processed with the same exchange procedure)

After receiving this information TCP will run all neccessary commands to get new ticket ready for issuing. All necessary additional documents are prepared at that stage, including Penalty EMD if applicable.

### 5. Finish exchange by issung ticket

You are all set!

Just use the [FinishExchange](./exchange/finish-exchange.md) method to issue new travel documents. Don't forget to mention if you want to issue EMD along with a ticket if you have chosen to create one.


### 6. Clean everything up

Don't forget to remove old segments. You may use [RemoveSegment](./exchange/remove-segment.md) method for this purpose.

## Special cases

You may also be interested how to exchange tickets in special cases like [involuntary rerouting](./exchange/involuntary-rerouting.md) or exchange [using manual mask](exchange/manual-mask.md). This cases are covered more deeply in the corresponding sections.
