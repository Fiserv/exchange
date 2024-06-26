---
tags: [Getting Started, Maintenance]
---
# Merchant Maintenance

## What is Merchant Maintenance?

When using exchange, you may want to update pricing after it has been boarded. In order to do this, a maintenance case must be created.

### Creating Maintenance Request

<!-- theme: info -->
>**POST** `/maintenance`

<!--
type: tab
titles: Request , Response 
-->

In order to create maintenance case, `/maintenance` endpoint must be used with operation_type : `CREATE_MAINTENANCE`. The user will need to provide the type of maintenance type `UPDATE_PROCESSING_PRICING`, and the `merchant_reference` for the submerchant. 
`merchant_reference` can be found by retrieving the merchant using the `boarding/merchant` [endpoint](../api/?type=post&path=/boarding/////merchant) , and the`internal_mid` of the level the pricing is on (usually merchant) should be retrieved for the next endpoint.  
In the response of the case creation, the  `old_details` will be provided,which can be used in the next endpoint to update. Please see the other tab for an example response for maintenance creation.

```json

{
  "operation": {
    "operation_type": "CREATE_MAINTENANCE"
  },
  "merchant": {
    "merchant_reference": "3016321"
  },
  "maintenance": {
    "maintenance_types": ["UPDATE_PROCESSING_PRICING"]
  }
}

```
<!-- type: tab -->

###  Response 

The response will provide the current details for the submerchant having the maintenance created for.

```json
{
    "result": "SUCCESS",
    "operation": {
        "operation_type": "CREATE_MAINTENANCE"
    },
    "maintenance": {
        "maintenance_reference": "MC3000000111",
        "merchant_reference": "3016321",
        "maintenance_status": "Open",
        "has_errors": "0",
        "maintenance_external_id": "MTNBE-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
        "creator_user_external_id": "USR4A-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
        "status_external_id": "MTS5F-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
        "owner_user_external_id": "USR4A-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX"
    },
    "maintenance_details": {
        "maintenance_reference": "MC3000000111",
        "merchant_reference": "3016321",
        "maintenance_types": [
            "UPDATE_PROCESSING_PRICING"
        ],
        "old_details": {
            "merchant": {
                "acquiringOffer": {
                    "transaction_pricing_external_id": "TPI01-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                    "transaction_pricing_id": "001",
                    "transaction_pricing_name": "Blended Offering",
                    "transaction_pricing_ref": "Standard Blended Offering",
                    "currency": "USD",
                    "is_tier_price": "0",
                    "tier_price_type": "1",
                    "fee_collection_type": "BLENDED",
                    "alliance_external_id": "ALL45-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                    "acquirer_external_id": "MAC85-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                    "processing_platform": "OTHER",
                    "charge_items": [
                        {
                            "charge_item_external_id": "CHI06-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                            "charge_item_id": "002",
                            "charge_item_name": "Blended Processing Rate",
                            "charge_item_ref": null,
                            "charge_item_group_external_id": "CIG93-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                            "charge_item_group_name": "Blended Rate",
                            "is_boarding_activated": "1",
                            "is_activated": "1",
                            "fee_collection_type": "BLENDED",
                            "mp_pricing_type_code": "10011",
                            "charge_decimals": "2",
                            "is_invisible": "0",
                            "tx_source": "1",
                            "is_mandatory": "1",
                            "is_merged_charges": "0",
                            "charge_item_prices": [
                                {
                                    "charge_item_price_charges": [
                                        {
                                            "tier_number": "0",
                                            "fee_type": "1",
                                            "category": "2",
                                            "base_charge": null,
                                            "default_base_charge": null,
                                            "minimum_base_charge": null,
                                            "maximum_base_charge": null,
                                            "perc_charge": "10.00",
                                            "default_perc_charge": "0.00000",
                                            "minimum_perc_charge": "0.00000",
                                            "maximum_perc_charge": "30.00000",
                                            "date_added": null,
                                            "date_updated": null
                                        },
                                        {
                                            "tier_number": "0",
                                            "fee_type": "2",
                                            "category": "2",
                                            "base_charge": "0.05",
                                            "default_base_charge": "0.00000",
                                            "minimum_base_charge": "0.00000",
                                            "maximum_base_charge": "9999.99000",
                                            "perc_charge": null,
                                            "default_perc_charge": null,
                                            "minimum_perc_charge": null,
                                            "maximum_perc_charge": null,
                                            "date_added": null,
                                            "date_updated": null
                                        }
                                    ],
                                    "date_added": null,
                                    "date_updated": null
                                }
                            ],
                            "date_added": null,
                            "date_updated": null
                        }
                    ],
                    "tiers": [],
                    "service_items": [
                        {
                            "service_charge_item_external_id": "SCI21-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                            "service_charge_item_id": "003",
                            "service_item_name": "Split to Third Party",
                            "service_ownership": "2",
                            "charge_ref": null,
                            "is_boarding_activated": "1",
                            "is_activated": "1",
                            "charge_decimals": "2",
                            "service_frequency": "7",
                            "is_invisible": "0",
                            "is_mandatory": "0",
                            "tx_source": "1",
                            "service_item_type": "1",
                            "occurrence_type": null,
                            "instalment_available": "2",
                            "service_item_charges": [
                                {
                                    "fee_type": "1",
                                    "base_charge": null,
                                    "default_base_charge": null,
                                    "minimum_base_charge": null,
                                    "maximum_base_charge": null,
                                    "perc_charge": "100.000",
                                    "default_perc_charge": null,
                                    "minimum_perc_charge": "0.00000",
                                    "maximum_perc_charge": "100.00000",
                                    "category": "2",
                                    "date_added": null,
                                    "date_updated": null
                                }
                            ],
                            "split_details": {
                                "target_merchant_id": "709900000101001",
                                "target_hierarchy_type": 1,
                                "target_node_id": "302321",
                                "date_added": null,
                                "date_updated": null
                            },
                            "date_added": null,
                            "date_updated": null
                        }
                    ],
                    "additional_data": [],
                    "date_added": null,
                    "date_updated": null
                }
            }
        }
    }
}
```
<!-- type: tab-end -->

### Updating Maintenance Case

<!-- theme: info -->
>**POST** `/maintenance`

Next, the maintenance case must be updated with the new information. Using the `old_details` from the Create maintenance case response, we can use this as a base to populate the new details to be updated.
For pricing, this will need to be added in the charges and acquring offer block. The `internal_mid` , `maintenance_reference` and `merchant reference` will need to be provided.
The actual rates will be updated by providing the new `perc_charge` and `base_charge` for the respective pricing being updated.

Example for updating the Blended rate, and split to third party. Data is taken from the old details in the response of the Maintenace creation, and the `perc_charge`, and `base_charge` are updated in the pricing below:

```json
{
    "operation": {
        "operation_type": "UPDATE_MAINTENANCE"
    },
    "merchant": {
        "merchant_reference": "3016321"
    },
    "maintenance": {
        "maintenance_reference": "MC3000000111",
        "merchant": {
            "internal_mid" :"700100000000001",
            "charges": {
                "acquiring_offer": {
                    "transaction_pricing_external_id": "TPI01-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                    "transaction_pricing_name": "Blended Offering",
                    "transaction_pricing_ref": "Standard Blended Offering",
                    "currency": "USD",
                    "is_tier_price": "0",
                    "tier_price_type": "1",
                    "fee_collection_type": "BLENDED",
                    "alliance_external_id": "ALL45-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                    "acquirer_external_id": "MAC85-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                    "processing_platform": "OTHER",
                    "charge_items": [
                        {
                            "charge_item_external_id": "CHI06-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                            "charge_item_name": "Blended Processing Rate",
                            "charge_item_ref": null,
                            "charge_item_group_external_id": "CIG93-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                            "charge_item_group_name": "Blended Rate",
                            "is_boarding_activated": "1",
                            "is_activated": "1",
                            "fee_collection_type": "BLENDED",
                            "mp_pricing_type_code": "10011",
                            "charge_decimals": "2",
                            "is_invisible": "0",
                            "tx_source": "1",
                            "is_mandatory": "1",
                            "is_merged_charges": "0",
                            "charge_item_prices": [
                                {
                                    "charge_item_price_charges": [
                                        {
                                            "tier_number": "0",
                                            "fee_type": "1",
                                            "category": "2",
                                            "perc_charge": "1.25",
                                            "default_perc_charge": "0.00000",
                                            "minimum_perc_charge": "0.00000",
                                            "maximum_perc_charge": "100.00000"
                                        },
                                        {
                                            "tier_number": "0",
                                            "fee_type": "2",
                                            "category": "2",
                                            "base_charge": "1.20",
                                            "default_base_charge": "0.00000",
                                            "minimum_base_charge": "0.00000",
                                            "maximum_base_charge": "9999.99000"

                                        }
                                    ]
                                }
                            ]
                        }
                    ],
                    "service_items": [
                        {
                            "service_charge_item_external_id": "SCI21-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                            "service_item_name": "Split to Third Party",
                            "service_ownership": "2",
                            "charge_ref": null,
                            "is_boarding_activated": "1",
                            "is_activated": "1",
                            "charge_decimals": "2",
                            "service_frequency": "7",
                            "is_invisible": "0",
                            "is_mandatory": "0",
                            "tx_source": "1",
                            "service_item_type": "1",
                            "occurrence_type": null,
                            "instalment_available": "2",
                            "service_item_charges": [
                                {
                                    "fee_type": "1",
                                    "perc_charge": "7.500",
                                    "default_perc_charge": null,
                                    "minimum_perc_charge": "0.00000",
                                    "maximum_perc_charge": "100.00000",
                                    "category": "2"
                                }
                            ],
                            "split_details": {
                                "target_merchant_id": "709900000101001",
                                "target_hierarchy_type": 1,
                                "target_node_id": "302321"
                            }
                        }
                    ]
                }
            }
        }
    }
}
```
### Submitting the Maintenance Case

<!-- theme: info -->
>**POST** `/maintenance`

Once this has been updated, we can now submit the case using the Maintenance reference number that was returned in the original Create Maintenance call. If succesful, merchant has now been updated with the new details.
Old details are send in the response under `old_details` , and new details under `/maintenance`

<!--
type: tab
titles: Request , Response 
-->
### Request: 

```json
{
  "operation": {
    "operation_type": "SUBMIT_MAINTENANCE"
  },
  "maintenance": {
    "maintenance_reference": "MC3000000111"
  }
}

```
<!-- type: tab -->

###  Response:

```json
{
    "result": "SUCCESS",
    "operation": {
        "operation_type": "SUBMIT_MAINTENANCE"
    },
    "maintenance": {
        "maintenance_reference": "MC3000000111",
        "merchant_reference": "302321",
        "maintenance_status": "Completed",
        "has_errors": 0,
        "maintenance_external_id": "MTN4B-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
        "creator_user_external_id": "USR4A-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
        "status_external_id": "MTS08-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
        "owner_user_external_id": "USR4A-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX"
    },
    "maintenance_details": {
        "maintenance_reference": "MC3000000111",
        "merchant_reference": "302321",
        "maintenance_types": [
            "UPDATE_PROCESSING_PRICING"
        ],
        "old_details": {
            "merchant": {
                "acquiringOffer": {
                    "transaction_pricing_external_id": "TPI01-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                    "transaction_pricing_id": "001",
                    "transaction_pricing_name": "Blended Offering",
                    "transaction_pricing_ref": "Standard Blended Offering",
                    "currency": "USD",
                    "is_tier_price": "0",
                    "tier_price_type": "1",
                    "fee_collection_type": "BLENDED",
                    "alliance_external_id": "ALL45-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                    "acquirer_external_id": "MAC85-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                    "processing_platform": "OTHER",
                    "charge_items": [
                        {
                            "charge_item_external_id": "CHI06-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                            "charge_item_id": "002",
                            "charge_item_name": "Blended Processing Rate",
                            "charge_item_ref": null,
                            "charge_item_group_external_id": "CIG93-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                            "charge_item_group_name": "Blended Rate",
                            "is_boarding_activated": "1",
                            "is_activated": "1",
                            "fee_collection_type": "BLENDED",
                            "mp_pricing_type_code": "10011",
                            "charge_decimals": "2",
                            "is_invisible": "0",
                            "tx_source": "1",
                            "is_mandatory": "1",
                            "is_merged_charges": "0",
                            "charge_item_prices": [
                                {
                                    "charge_item_price_charges": [
                                        {
                                            "tier_number": "0",
                                            "fee_type": "1",
                                            "category": "2",
                                            "base_charge": null,
                                            "default_base_charge": null,
                                            "minimum_base_charge": null,
                                            "maximum_base_charge": null,
                                            "perc_charge": "10.00",
                                            "default_perc_charge": "0.00000",
                                            "minimum_perc_charge": "0.00000",
                                            "maximum_perc_charge": "30.00000",
                                            "date_added": null,
                                            "date_updated": null
                                        },
                                        {
                                            "tier_number": "0",
                                            "fee_type": "2",
                                            "category": "2",
                                            "base_charge": "0.05",
                                            "default_base_charge": "0.00000",
                                            "minimum_base_charge": "0.00000",
                                            "maximum_base_charge": "9999.99000",
                                            "perc_charge": null,
                                            "default_perc_charge": null,
                                            "minimum_perc_charge": null,
                                            "maximum_perc_charge": null,
                                            "date_added": null,
                                            "date_updated": null
                                        }
                                    ],
                                    "date_added": null,
                                    "date_updated": null
                                }
                            ],
                            "date_added": null,
                            "date_updated": null
                        }
                    ],
                    "tiers": [],
                    "service_items": [
                        {
                            "service_charge_item_external_id": "SCI21-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                            "service_charge_item_id": "003",
                            "service_item_name": "Split to Third Party",
                            "service_ownership": "2",
                            "charge_ref": null,
                            "is_boarding_activated": "1",
                            "is_activated": "1",
                            "charge_decimals": "2",
                            "service_frequency": "7",
                            "is_invisible": "0",
                            "is_mandatory": "0",
                            "tx_source": "1",
                            "service_item_type": "1",
                            "occurrence_type": null,
                            "instalment_available": "2",
                            "service_item_charges": [
                                {
                                    "fee_type": "1",
                                    "base_charge": null,
                                    "default_base_charge": null,
                                    "minimum_base_charge": null,
                                    "maximum_base_charge": null,
                                    "perc_charge": "100.000",
                                    "default_perc_charge": null,
                                    "minimum_perc_charge": "0.00000",
                                    "maximum_perc_charge": "100.00000",
                                    "category": "2",
                                    "date_added": null,
                                    "date_updated": null
                                }
                            ],
                            "split_details": {
                                "target_merchant_id": "709900000101001",
                                "target_hierarchy_type": 1,
                                "target_node_id": "302321",
                                "date_added": null,
                                "date_updated": null
                            },
                            "date_added": null,
                            "date_updated": null
                        }
                    ],
                    "additional_data": [],
                    "date_added": null,
                    "date_updated": null
                },
        "new_details": {
            "merchant": {
                "acquiringOffer": {
                    "transaction_pricing_external_id": "TPI01-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                    "transaction_pricing_id": "001",
                    "transaction_pricing_name": "Blended Offering",
                    "transaction_pricing_ref": "Standard Blended Offering",
                    "currency": "USD",
                    "is_tier_price": "0",
                    "tier_price_type": "1",
                    "fee_collection_type": "BLENDED",
                    "alliance_external_id": "ALL45-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                    "acquirer_external_id": "MAC85-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                    "processing_platform": "OTHER",
                    "charge_items": [
                        {
                            "charge_item_external_id": "CHI06-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                            "charge_item_id": "002",
                            "charge_item_name": "Blended Processing Rate",
                            "charge_item_ref": null,
                            "charge_item_group_external_id": "CIG93-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                            "charge_item_group_name": "Blended Rate",
                            "is_boarding_activated": "1",
                            "is_activated": "1",
                            "fee_collection_type": "BLENDED",
                            "mp_pricing_type_code": "10011",
                            "charge_decimals": "2",
                            "is_invisible": "0",
                            "tx_source": "1",
                            "is_mandatory": "1",
                            "is_merged_charges": "0",
                            "charge_item_prices": [
                                {
                                    "charge_item_price_charges": [
                                        {
                                            "tier_number": "0",
                                            "fee_type": "1",
                                            "category": "2",
                                            "base_charge": null,
                                            "default_base_charge": null,
                                            "minimum_base_charge": null,
                                            "maximum_base_charge": null,
                                            "perc_charge": "1.25",
                                            "default_perc_charge": "0.00000",
                                            "minimum_perc_charge": "0.00000",
                                            "maximum_perc_charge": "30.00000",
                                            "date_added": null,
                                            "date_updated": null
                                        },
                                        {
                                            "tier_number": "0",
                                            "fee_type": "2",
                                            "category": "2",
                                            "base_charge": "1.20",
                                            "default_base_charge": "0.00000",
                                            "minimum_base_charge": "0.00000",
                                            "maximum_base_charge": "9999.99000",
                                            "perc_charge": null,
                                            "default_perc_charge": null,
                                            "minimum_perc_charge": null,
                                            "maximum_perc_charge": null,
                                            "date_added": null,
                                            "date_updated": null
                                        }
                                    ],
                                    "date_added": null,
                                    "date_updated": null
                                }
                            ],
                            "date_added": null,
                            "date_updated": null
                        }
                    ],
                    "tiers": [],
                    "service_items": [
                        {
                            "service_charge_item_external_id": "SCI21-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                            "service_charge_item_id": "003",
                            "service_item_name": "Split to Third Party",
                            "service_ownership": "2",
                            "charge_ref": null,
                            "is_boarding_activated": "1",
                            "is_activated": "1",
                            "charge_decimals": "2",
                            "service_frequency": "7",
                            "is_invisible": "0",
                            "is_mandatory": "0",
                            "tx_source": "1",
                            "service_item_type": "1",
                            "occurrence_type": null,
                            "instalment_available": "2",
                            "service_item_charges": [
                                {
                                    "fee_type": "1",
                                    "base_charge": null,
                                    "default_base_charge": null,
                                    "minimum_base_charge": null,
                                    "maximum_base_charge": null,
                                    "perc_charge": "7.500",
                                    "default_perc_charge": null,
                                    "minimum_perc_charge": "0.00000",
                                    "maximum_perc_charge": "100.00000",
                                    "category": "2",
                                    "date_added": null,
                                    "date_updated": null
                                }
                            ],
                            "split_details": {
                                "target_merchant_id": "709900000101001",
                                "target_hierarchy_type": 1,
                                "target_node_id": "302321",
                                "date_added": null,
                                "date_updated": null
                            },
                            "date_added": null,
                            "date_updated": null
                        }
                    ],
                    "additional_data": [],
                    "date_added": null,
                    "date_updated": null
                }
    }
}
```
<!-- type: tab-end -->


