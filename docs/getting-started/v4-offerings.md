# Product Offers

Product offers group pricing, gateways, and billing items within Exchange to be added during boarding. These are configured on the config portal, to be retrieved by a set of APIs - which are then added to your boarding requests. The product codes may change between environments, but once created identifier will remain the same.

## List Offers

<!-- theme: info -->
>**POST** `/product_offer/list`

The user can retrieve all available offers to their setup to them by using the List offer API. Using an empty payload will retrieve all available offers, or criteria can be provided to filter this down if your setup has partners setup. Offer code will be used in the retrieve endpoint to get all detail of the offer.

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

## Retrieve Offer

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

Key fields in the response include: 

| **Field**                             | **Type**          | **Description**                                                                                                                                       |
|---------------------------------------|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| `offer.offer_name`                    | String            | Name of the offer. Example: `"Sample Offer"`                                                                                                          |
| `offer.offer_code`                    | String            | Unique code of the offer, system generated. Example: `"PRO00000000001"`                                                                               |
| `offer.product_items`                 | Array of Objects  | List of product items related to the offer. Product items include pricing, billing, gateways.                                                         |
| `offer.product_items.product_name`    | String            | Name of the product. Example: `"Gateway"`                                                                                                             |
| `offer.product_items.product_code`    | String            | Product code of the product. Example: `"54321"`                                                                                                        |
| `offer.product_items.relate_to`       | String            | Defines what the product relates to in the system.  Example: `"NORTH_GATEWAY_EQUIPMENT"`                                                                              |
| `offer.product_items.max_percentage_amount` | String            | Maximum percentage amount for the product, configured in the config portal. Example: `"0.00000"`                                                        |
| `offer.product_items.max_fixed_amount`| String            | Maximum fixed amount for the product, configured in the config portal. Example: `"0.00000"`                                                            |
| `offer.entitlements`                  | Array of Objects  | List of entitlements associated with the offer, based on how the offer has been configured.                                                            |
| `offer.entitlements.entitlement_key`  | String            | Key of the entitlement. Example: `"VISA"`                                                                                                              |


Please see full spec on the API explorer [endpoint](../api/?type=post&path=/product_offer/retrieve)

## Adding an Offer during Boarding

Once details are retrieved, these can be added to the boarding APIs under the offer block. Typically, this will be added on the Location (Outlet) level under the offer item. An example of an offer payload that could be added to a location during boarding would look like below, after retrieving the information required.
This would add the gateway with `product_code` `GTWY01` , and Entitlements for Visa and Mastercard.

```json
    "offer": {
      "product_offer_code": "PRO00000000001",
      "product_items": [
        {
          "product_code": "GTWY01",
          "quantity": "1"
        }
      ],
      "entitlements": [
        {
          "entitlement_key": "VISA"
        },
        {
          "entitlement_key": "MASTERCARD"
        }
      ]
    }
```
