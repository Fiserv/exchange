
---
tags: [Getting Started, Maintenance, Boarding]
---
# DBA Maintenance

Exchange allows boarding of sub-merchants on the system. Once on-boarded, 

## Updating DBA info

To update DBA info for an existing sub-merchant, a Maintenance case must be created, updated and submit. 
The following fields may  be updated for a location with this case: 

* `primary_email_address`
*  `outlet_website`
*  `trade_name`

### Creating the case

<!-- theme: info -->
>**POST** `/maintenance`

The`CHANGE_DBA` maintenance type must be used, and `merchant_reference` must be provided to create the case.

This returns a `maintenance_reference`, and the `old_details` 


```json
{
    "result": "SUCCESS",
    "operation": {
        "operation_type": "CREATE_MAINTENANCE"
    },
    "maintenance": {
        "maintenance_reference": "MC5000000001",
        "merchant_reference": "5000001",
        "maintenance_status": "Open",
        "has_errors": "0",
        "maintenance_external_id": "MTBCD-C475E-82BE7-B1AA4-9A026-89381-4EA08",
        "creator_user_external_id": "USBCD-C475E-82BE7-B1AA4-9A026-89381-4EA08",
        "status_external_id": "MTS5F-C475E-82BE7-B1AA4-9A026-89381-4EA08",
        "owner_user_external_id": "USABC-C475E-82BE7-B1AA4-9A026-89381-4EA08"
    },
    "settings": {
        "funding_flag": "0",
        "billing_flag": "0",
        "reserve_flag": "0",
        "526030471886": {
            "billing": {
                "billing_frequency": "0",
                "billing_day": "0",
                "billing_month": "0",
                "has_transaction_billing": "0",
                "tx_fees_billing_method": "0",
                "other_fees_billing_method": "2",
                "has_equipment_billing": "0",
                "has_service_billing": "0"
            },
            "funding": {
                "funding_frequency": "0",
                "funding_day": "0",
                "funding_month": "0",
                "delay_funding_flag": "0",
                "settlement_method": "0",
                "tx_instruction_on": "0",
                "tx_source_ach": "0",
                "tx_source_card": "1",
                "tx_source_ach_funding_option": "0",
                "tx_source_ach_settlement_method": "0",
                "tx_source_card_funding_option": "2",
                "tx_source_card_settlement_method": "2"
            },
            "reserve": {
                "set_reserve_target": "0"
            }
        }
    },
    "maintenance_details": {
        "maintenance_reference": "MC5000000001",
        "merchant_reference": "5000001",
        "maintenance_types": [
            "CHANGE_DBA"
        ],
        "old_details": {
            "outlets": {
                "6c933e018965d93e0147": {
                    "primary_email_address": "testaddress@fiserv.com",
                    "outlet_website": "https://fiserv.com",
                    "trade_name": "MMISTEST Tradename"
                }
            }
        }
    }
}
```

### Updating the DBA Case

<!-- theme: info -->
>**POST** `/maintenance`

<!--
type: tab
titles: Request , Response
-->

### Auto-Funding Request 

The reserve settings must be added on the funding/billing level of the sub-merchant. This will usually be at the location (outlet) level, but can also be on the Merchant or chain (subgroup).  The settings you want to set the reserve up with will need to be provided, and the system will start collecting amounts at the next available cycle after the case is completed. 

```json
{
    "operation": {
        "operation_type": "UPDATE_MAINTENANCE"
    },
    "merchant": {
        "merchant_reference": "5000001"
    },
    "maintenance": {
        "maintenance_reference": "MC5000000001",
        "outlets": [
            {
                "internal_mid": "321000071001",
                "primary_email_address": "newemail@fiserv.com",
                "outlet_website": "https://developer.fiserv.com/product/exchange",
                "trade_name": "MMISTEST NewDBA"
            }
        ]
    }
}

---


<!-- type: tab -->

### Response

The reserve settings must be added on the funding/billing level of the sub-merchant. This will usually be at the outlet level, but can also be on the Merchant or subgroup.
For an instructional funding setup, the reserve would need to be enabled only. No settings would be applicable as these are collected by instructions.

```json
{
    "result": "SUCCESS",
    "operation": {
        "operation_type": "UPDATE_MAINTENANCE"
    },
    "maintenance": {
        "maintenance_reference": "MC5000000001",
        "merchant_reference": "5000001",
        "maintenance_status": "Open",
        "has_errors": "0",
        "maintenance_external_id": "MTBCD-C475E-82BE7-B1AA4-9A026-89381-4EA08",
        "creator_user_external_id": "USBCD-C475E-82BE7-B1AA4-9A026-89381-4EA08",
        "status_external_id": "MTS5F-C475E-82BE7-B1AA4-9A026-89381-4EA08",
        "owner_user_external_id": "USABC-C475E-82BE7-B1AA4-9A026-89381-4EA08"
    },
    "settings": {
        "funding_flag": "0",
        "billing_flag": "0",
        "reserve_flag": "0",
        "526030471886": {
            "billing": {
                "billing_frequency": "0",
                "billing_day": "0",
                "billing_month": "0",
                "has_transaction_billing": "0",
                "tx_fees_billing_method": "0",
                "other_fees_billing_method": "2",
                "has_equipment_billing": "0",
                "has_service_billing": "0"
            },
            "funding": {
                "funding_frequency": "0",
                "funding_day": "0",
                "funding_month": "0",
                "delay_funding_flag": "0",
                "settlement_method": "0",
                "tx_instruction_on": "0",
                "tx_source_ach": "0",
                "tx_source_card": "1",
                "tx_source_ach_funding_option": "0",
                "tx_source_ach_settlement_method": "0",
                "tx_source_card_funding_option": "2",
                "tx_source_card_settlement_method": "2"
            },
            "reserve": {
                "set_reserve_target": "0"
            }
        }
    },
    "maintenance_details": {
        "maintenance_reference": "MC5000000001",
        "merchant_reference": "5000001",
        "maintenance_types": [
            "CHANGE_DBA"
        ],
        "old_details": {
            "outlets": {
                "6c933e018965d93e0147": {
                    "primary_email_address": "testaddress@fiserv.com",
                    "outlet_website": "https://fiserv.com",
                    "trade_name": "MMISTEST Tradename"
                }
            }
        },
        "new_details": {
            "outlets": {
                "6c933e018965d93e0147": {
                "primary_email_address": "newemail@fiserv.com",
                "outlet_website": "https://developer.fiserv.com/product/exchange",
                "trade_name": "MMISTEST NewDBA"
            }
            }
        }
    }
}
```
                                                      
---
<!-- type: tab-end -->


### Submitting the Case

<!-- theme: info -->
>**POST** `/maintenance`

Once the case has been updated with the settings for the Reserve, it must be submitted using the `maintenance_reference`.
Once submitted, a `"maintenance_status"`: "Completed" means the maintenance is complete, and the reserve has been added.

```json
{
    "operation": {
        "operation_type": "SUBMIT_MAINTENANCE"
    },
    "maintenance": {
        "maintenance_reference": "MC3000000001"
    }
}
```

### Retrieving the Case

<!-- theme: info -->
>**POST** `/maintenance`

The initial `"maintenance_status"` will be `Awaiting Maintenance Marketplace Boarding` , and can be expected to move to `Completed` within an hour. 
The maintenance case can be retrieved to review the details, and to check on the `maintenance_status`.

```json
{
    "result": "SUCCESS",
    "operation": {
        "operation_type": "RETRIEVE_MAINTENANCE"
    },
    "maintenance": {
        "maintenance_reference": "MC5000001001",
        "merchant_reference": "5001001",
        "maintenance_status": "Awaiting Maintenance Marketplace Boarding",
        "has_errors": "0",
        "maintenance_external_id": "MTXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
        "creator_user_external_id": "USXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
        "status_external_id": "MTXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
        "owner_user_external_id": "USXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX"
    },
    "settings": {
        "funding_flag": "0",
        "billing_flag": "0",
        "reserve_flag": "0",
        "526030471886": {
            "billing": {
                "billing_frequency": "0",
                "billing_day": "0",
                "billing_month": "0",
                "has_transaction_billing": "0",
                "tx_fees_billing_method": "0",
                "other_fees_billing_method": "2",
                "has_equipment_billing": "0",
                "has_service_billing": "0"
            },
            "funding": {
                "funding_frequency": "0",
                "funding_day": "0",
                "funding_month": "0",
                "delay_funding_flag": "0",
                "settlement_method": "0",
                "tx_instruction_on": "0",
                "tx_source_ach": "0",
                "tx_source_card": "1",
                "tx_source_ach_funding_option": "0",
                "tx_source_ach_settlement_method": "0",
                "tx_source_card_funding_option": "2",
                "tx_source_card_settlement_method": "2"
            },
            "reserve": {
                "set_reserve_target": "0"
            }
        }
    },
    "maintenance_details": {
        "maintenance_reference": "MC5000001001",
        "merchant_reference": "5001001",
        "maintenance_types": [
            "CANCEL_LOCATION"
        ],
        "cancel_location_details": {
            "location_to_cancel": "325000100001",
            "cancellation_reason": "Cancelled"
        },
        "orderId": "xe001"
    }
}
```

| maintenance_status Responses             | Data Type | Description                                                                                                                                    |
|-------------------------|-----------|------------------------------------------------------------------------------------------------------------------------------------------------|
| `Awaiting Maintenance Marketplace Boarding`      | String   |  Initial transient status for submission downstream.                                                                        |
| `Awaiting Maintenance Marketplace Response`      | String   |  Maintenance details submit downstream and confirmation. Adds `orderId` into `maintenance_details`.                                                              |
| `Completed`      | String   |  Maintenance case has completed, and synced.                                                                        |
| `Partially Applied`      | String   |  Only applicable for maintenance cases that have more than `maintenance_types` , which affect a merchant in downstream systems as well as a maintenance type that is only applied within exchange. If the case is cancelled before the dowstream syncs are complete, the case is marked as partially applied.                                                                        |
