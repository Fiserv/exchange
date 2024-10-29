
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
```

| Field Name              | Data Type | Description                                                                                                                                    |
|-------------------------|-----------|------------------------------------------------------------------------------------------------------------------------------------------------|
| `take_reserves_flag`      | Integer   | Flag indicating whether to take reserves (1 for true, 0 for false).                                                                            |
| `reserve_type`            | Integer   | Type of reserve being configured. 1 - Normal, 2 - Rolling.                                                                                     |
| `reserve_setting`         | Integer   | Reserve collection setting. 1 - Percentage, 2 - Base.                                                                                          |
| `reserve_daily_amount`    | Integer   | Amount to be collected daily. Used for reserve_setting = 2 (Base), specifies the daily amount taken into reserve for the sub-merchant.         |
| `reserve_trans_perc`      | Integer   | Used for reserve_setting = 1 (Percentage). Specifies the percentage taken out of the transactions for the sub-merchant.                        |
| `set_reserve_target`      | Integer   | Flag indicating whether to set a reserve target (1 for true, 0 for false). Will enable reserve_target_amount to be set for the sub-merchant.   |
| `reserve_target_amount`   | Integer   | Maximum amount to collect for the sub-merchant when set_reserve_target is true.                                                                 |
| `reserve_delay_days`      | Integer   | Used for reserve_type = 2 (Rolling). Sets the period of time for the rolling reserve to release amounts. Max 90.                                        |

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

| Field Name              | Data Type | Description                                                                                                                                    |
|-------------------------|-----------|------------------------------------------------------------------------------------------------------------------------------------------------|
| `take_reserves_flag`      | Integer   | Flag indicating whether to take reserves (1 for true, 0 for false).                                                                            |
| `reserve_type`            | Integer   | Type of reserve being configured. 1 - Normal, 2 - Rolling.                                                                                     |
| `set_reserve_target`      | Integer   | Flag indicating whether to set a reserve target (1 for true, 0 for false). Will enable `reserve_target_amount` to be set for the sub-merchant.  |
| `reserve_target_amount`   | Integer   | Maximum amount to collect for the sub-merchant when `set_reserve_target` is true.                                                              |
                                                          
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
