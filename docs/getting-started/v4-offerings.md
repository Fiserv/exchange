# Product Offers

Product offers group pricing, gateways, and billing items within exchange to be added during boarding. These are configured on the config portal, to be retrieved by a set of APIs - which are then added to your boarding requests.

## List offers

<!-- theme: info -->
>**POST** `/product_offer/list`

The user can retrieve all available offers to their setup to them by using the List offer API. Using an empty payload will retrieve all available offers, or criteria can be provided to filter this down if your setup has partners setup.

## Retrieve offer

<!-- theme: info -->
>**POST** `/product_offer/retrieve`

After listing the offers, you can retrieve the full details of a selected one by using the `offer_code` , in the retrieve product offer API

## Adding into boarding

Now, once details retrieved, this can be added to the boarding APIs under the offer block. Typically, entitlements will be added in the add_application level and the gateway to process transactions added in the add_outlet api.

