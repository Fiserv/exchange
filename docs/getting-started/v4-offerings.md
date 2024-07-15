# Product Offers

Product offers group pricing, gateways, and billing items within exchange to be added during boarding. These are configured on the config portal, to be retrieved by a set of APIs - which are then added to your boarding requests.

## List offers

<!-- theme: info -->
>**POST** `/product_offer/list`

The user can retrieve all available offers to their setup to them by using the List offer API. Using an empty payload will retrieve all available offers, or criteria can be provided to filter this down if your setup has partners setup.

Sample Response : 

```json
{
    "result": "SUCCESS",
    "product_offers": [
        {
            "client_code": "FISERV",
            "alliance_code": "SAMPLE",
            "partner_code": "SAMPLE",
            "division_id": "USA",
            "offer_name": "Sample Offer",
            "offer_reference": "SMPO1",
            "offer_code": "PRO00000000001",
            "currency": "USD",
            "status": "1",
            "date_added": "2022-01-12 09:15:00"
        }
    ]
}
```

## Retrieve offer

<!-- theme: info -->
>**POST** `/product_offer/retrieve`

After listing the offers, you can retrieve the full details of a selected one by using the `offer_code` , in the retrieve product offer API

Sample Request: 

```json
{
"offer_code" : "PRO00000000001"
}
```

Sample Response: 

```json
{
    "result": "SUCCESS",
    "offer": {
        "offer_name": "Sample Offer",
        "offer_reference": "SMP01",
        "offer_code": "PRO00000000001",
        "currency": "USD",
        "status": "1",
        "date_added": "2022-12-01 09:15:00",
        "product_items": [
            {
                "product_name": "Gateway",
                "product_code": "54321",
                "relate_to": "NORTH_GATEWAY_EQUIPMENT",
                "tx_source": "1",
                "max_percentage_amount": "0.00000",
                "max_fixed_amount": "0.00000",
                "attributes": []
            }
        ],
        "entitlements": [
            {
                "entitlement_name": "Visa",
                "entitlement_key": "VISA",
                "entitlement_type": "Entitlement"
            },
            {
                "entitlement_name": "Discover",
                "entitlement_key": "DISCOVER",
                "entitlement_type": "Entitlement"
            },
            {
                "entitlement_name": "Mastercard",
                "entitlement_key": "MASTERCARD",
                "entitlement_type": "Entitlement"
            },
            {
                "entitlement_name": "AMEX Opt Blue",
                "entitlement_key": "AMEX",
                "entitlement_type": "Entitlement"
            }
        ]
    }
}
```

## Adding into boarding

Now, once details retrieved, this can be added to the boarding APIs under the offer block. Typically, entitlements will be added in the add_application level and the gateway to process transactions added in the add_outlet api.


