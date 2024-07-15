# Product Offers

Product offers group pricing, gateways, and billing items within exchange to be added during boarding. These are configured on the config portal, to be retrieved by a set of APIs - which are then added to your boarding requests.

## List offers

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
| **Field**                             | **Type**          | **Description**                                                                                                                                       |
|---------------------------------------|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| `result`                              | String            | Status of the API call. Example: `"SUCCESS"`                                                                                                          |
| `offer`                               | Object            | Contains details about the offer                                                                                                                      |
| `offer.offer_name`                    | String            | Name of the offer. Example: `"Sample Offer"`                                                                                                          |
| `offer.offer_reference`               | String            | Reference of the offer, defined in the config portal. Example: `"SMP01"`                                                                              |
| `offer.offer_code`                    | String            | Unique code of the offer, system generated. Example: `"PRO00000000001"`                                                                               |
| `offer.currency`                      | String            | Currency code for the offer. Example: `"USD"`                                                                                                         |
| `offer.status`                        | String            | Status of the offer. 1 is Active. Example: `"1"`                                                                                                       |
| `offer.date_added`                    | String (DateTime) | Date and time the offer was added. Example: `"2022-12-01 09:15:00"`                                                                                    |
| `offer.product_items`                 | Array of Objects  | List of product items related to the offer. Product items include pricing, billing, gateways.                                                         |
| `offer.product_items.product_name`    | String            | Name of the product. Example: `"Gateway"`                                                                                                             |
| `offer.product_items.product_code`    | String            | Product code of the product. Example: `"54321"`                                                                                                        |
| `offer.product_items.relate_to`       | String            | Defines what the product relates to. Example: `"NORTH_GATEWAY_EQUIPMENT"`                                                                              |
| `offer.product_items.tx_source`       | String            | Transaction source associated with the product. Used for setups where multiple sources through exchange are consumed. Example: `"1"`                    |
| `offer.product_items.max_percentage_amount` | String            | Maximum percentage amount for the product, configured in the config portal. Example: `"0.00000"`                                                        |
| `offer.product_items.max_fixed_amount`| String            | Maximum fixed amount for the product, configured in the config portal. Example: `"0.00000"`                                                            |
| `offer.product_items.attributes`      | Array of Objects  | List of attributes related to the product. Used for sending attributes for products, applicable for setups sending Auto close time, transarmor.        |
| `offer.entitlements`                  | Array of Objects  | List of entitlements associated with the offer, based on how the offer has been configured.                                                            |
| `offer.entitlements.entitlement_name` | String            | Name of the entitlement. Example: `"Visa"`                                                                                                             |
| `offer.entitlements.entitlement_key`  | String            | Key of the entitlement. Example: `"VISA"`                                                                                                              |
| `offer.entitlements.entitlement_type` | String            | Type of the entitlement. Example: `"Entitlement"`. Other types reserved for future use.                                                               |


Please see full spec on the API explorer [endpoint](../api/?type=post&path=/boarding/////merchant)

## Adding into boarding

Once details are retrieved, this can be added to the boarding APIs under the offer block. Typically, this will be added on the outlet level under the offer item.


