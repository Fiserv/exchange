---
tags: [Getting Started, Maintenance]
---
# Merchant Maintenance

## What is Merchant Maintenance?

When using exchange, you may want to update submerchant data or pricing after it has been boarded. In order to do this, a maintenance case must be created.

## General Maintenance process

The user will be able to create a merchant maintenance case with the type of maintenance they would like to do, have this updated, and then submit the case.
This is primarily be facilitated through the `/maintenance` endpoint.

### Creating Maintenance Case

<!-- theme: info -->
>**POST** `/maintenance`

In order to create maintenance case, `/maintenance` endpoint must be used with operation_type : `CREATE_MAINTENANCE`. The user will need to provide the type of maintenance being performed, and the `merchant_reference` for the submerchant. 
The `old_details` will provide the data being updated, which can be used in the next endpoint to update.
`merchant_reference` can be found by retrieving the merchant using the `boarding/merchant` [endpoint](../api/?type=post&path=/boarding/////merchant)

Example request body:
```
{
  "operation": {
    "operation_type": "CREATE_MAINTENANCE"
  },
  "merchant": {
    "merchant_reference": "3001001"
  },
  "maintenance": {
    "maintenance_types": ["CHANGE_BANK"]
  }
}
```
### Updating Maintenance Case

<!-- theme: info -->
>**POST** `/maintenance`


Next, the maintenance case must be updated with the new information. Using the `old_details` from the Create maintenance case response, we can use this as a base to populate the new details to be updated.
Depending on the maintenance case, you will need to include the new details in their respective block in the request. ie, banks for Bank changes. Please see [examples](../api/?type=post&path=//maintenance) on the request page for more info

Example for bank change below:
```
{
  "operation": {
    "operation_type": "UPDATE_MAINTENANCE"
  },
  "merchant": {
    "merchant_reference": "3001001"
  },
  "maintenance": {
    "outlets": {
      "maintenance_reference": "MC3000000601",
      "internal_mid": "7001000000500001",
      "banks": [
        {
          "_id": "12b5534faf9baf2232bb23c",
          "bank_name": "Bank of Test",
          "country_code": "840",
          "zip_code": "12345",
          "county_code": "CA",
          "account_holder_name": "Jane Doe",
          "bank_account_type": "CHECKING",
          "dda_number": "123456789",
          "routing_number": "333456789",
          "account_type": [
            "CREDIT",
            "DEBIT",
            "CHARGEBACK"
          ]
        }
      ]
    }
  }
}
```
### Submitting the Maintenance Case

<!-- theme: info -->
>**POST** `/maintenance`

Once this has been updated, we can now submit the case using the Maintenance reference number that was returned in the original Create Maintenance call. If succesful, merchant has now been updated with the new details.
```
{
  "operation": {
    "operation_type": "SUBMIT_MAINTENANCE"
  },
  "maintenance": {
    "maintenance_reference": "MC3000000601"
  }
}

```
### Cancelling a Maintenance Case

<!-- theme: info -->
>**POST** `/maintenance`


Only one maintenance case can be open at a time. If you need to cancel a case, the `MAINTENANCE_CANCEL` operation type should be used.
<!--
type: tab
titles: Request , Response 
-->
### Request: 

```json
{
  "operation": {
    "operation_type": "MAINTENANCE_CANCEL"
  },
  "maintenance": {
    "maintenance_reference": "MC3000000601"
  }
}

```
<!-- type: tab -->

###  Response:

```json
{
    "result": "SUCCESS",
    "operation": {
        "operation_type": "MAINTENANCE_CANCEL"
    },
    "message": "Maintenance Case Successfully Cancelled"
}

```
<!-- type: tab-end -->

### Searching for Maintenance Cases

<!-- theme: info -->
>**POST** `/maintenance`

Maintenance cases for a merchant can be searched using the `MAINTENANCE_SEARCH` operation. This allows the user to retrieve all current and previous maintenance cases made for a submerchant. The `maintenance_status` can be used to view what state the case is in.

<!--
type: tab
titles: Request , Response 
-->
### Request: 

```json

{
  "operation": {
    "operation_type": "MAINTENANCE_SEARCH"
  },
  "search": {
    "page": "1",
    "limit": "50",
    "merchant_reference": "3001001"
  }
}

```
<!-- type: tab -->

###  Response:

```json
{
    "result": "SUCCESS",
    "operation": {
        "operation_type": "MAINTENANCE_SEARCH"
    },
    "response": {
        "limit": "50",
        "page": "1",
        "summary_status": "FOUND",
        "maintenance": [
            {
                "maintenance_reference": "MC3000000601",
                "maintenance_types": [
                    "UPDATE_PROCESSING_PRICING"
                ],
                "merchant_reference": "3001001",
                "business_legal_name": "MMISTest Legal name",
                "parent_type": "ALLIANCE",
                "contact_first_name": "Jane",
                "contact_last_name": "Doe",
                "date_added": "2022-02-12 14:48:41",
                "maintenance_external_id": "MTN4B-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                "creator_user_external_id": "USR4A-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                "status_external_id": "MTS08-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX"",
                "maintenance_status": "Completed",
                "owner_user_external_id": "USR4A-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX""
            },
            {
                "maintenance_reference": "MC3000000600",
                "maintenance_types": [
                    "UPDATE_PROCESSING_PRICING"
                ],
                "merchant_reference": "3001001",
                "business_legal_name": "MMISTest Legal name",
                "parent_type": "ALLIANCE",
                "contact_first_name": "Jane",
                "contact_last_name": "Doe",
                "date_added": "2022-02-12 13:22:23",
                "maintenance_external_id": "MTNBE-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX"",
                "creator_user_external_id": "USR4A-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX"",
                "status_external_id": "MTSF8-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX"",
                "maintenance_status": "Cancelled",
                "owner_user_external_id": "USR4A-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX""
            }
        ]
    }
}

```
<!-- type: tab-end -->

### Retrieve Maintenance Cases

<!-- theme: info -->
>**POST** `/maintenance`

Specific Maintenance cases for a merchant can be pulled using the `RETRIEVE_MAINTENANCE` operation. This allows the user to retrieve a specific maintenance case made for a submerchant. 

<!--
type: tab
titles: Request , Response 
-->
### Request: 

```json

{
 
  "operation": {
    "operation_type": "RETRIEVE_MAINTENANCE"
  },
  "maintenance": {
    "maintenance_reference": "MC3000000601"
  }
}


```
<!-- type: tab -->

###  Response:

```json
{
    "result": "SUCCESS",
    "operation": {
        "operation_type": "RETRIEVE_MAINTENANCE"
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
