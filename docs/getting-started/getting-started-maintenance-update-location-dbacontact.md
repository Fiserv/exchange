
---
tags: [Getting Started, Maintenance, Reserves]
---

# Reserve Maintenance

Reserves can be added to sub-merchants to collect and manage amounts for collateral through Exchange. For Auto-Funding, this can be used to setup a reserve to collect automatically based on settings. For Instructional funding, reserves can be enabled and collected with funding instructions. Only one maintenance case for reserves on a sub-merchant can be active at a time.

## Updating a Reserve

Reserve settings can be updated for a sub-merchant. This can be used to update how the reserve collects for Auto-Funding, or to raise the collection amount for the reserve. This can also be used to stop collecting reserves from a sub-merchant but retain the current reserve balance for future use.

### Creating the case

<!-- theme: info -->
>**POST** `/maintenance`

The `AMEND_RESERVE` maintenance type must be used, and `merchant_reference` must be provided to create the case.

This returns a `maintenance_reference`, unique to this case which can then be updated.

```json
{
    "result": "SUCCESS",
    "operation": {
        "operation_type": "CREATE_MAINTENANCE"
    },
    "maintenance": {
        "maintenance_reference": "MC5000001001",
        "merchant_reference": "5001001",
        "maintenance_status": "Open",
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
        "526023475886": {
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
            "CHANGE_DBA_CONTACT"
        ],
        "old_details": {
            "outlets": {
                "ad42966777630006671f6f7d": {
                    "contacts": {
                        "ad42966777630006671f6bcd": {
                            "contact_type": "OT",
                            "contact_first_name": "Jane",
                            "contact_last_name": "Doe",
                            "country_code": "840",
                            "city": "Sparks",
                            "zip_code": "89431",
                            "street_line_1": "Sheila Lane",
                            "county_code": "NV",
                            "email_address": "email@domain.com",
                            "ent_telephone_code": "US|1",
                            "telephone_number": "3339898989"
                        }
                    }
                }
            }
        }
    }
}
```

### Updating the Reserve 

<!-- theme: info -->
>**POST** `/maintenance`

Using the `maintenance_reference`, the case can then be updated and the new settings can be provided. The case must be updated on the same level as the original reserve, so if it was previously set on the "location" (outlet) , then it must still be updated on the location (outlet).

When updating a reserve, all settings can be updated. If reserves are no longer to be collected, but the reserve balance retained, whichever has been set from `"reserve_daily_amount"` or `"reserve_trans_perc"` should be set to `“0”`.
 
```json
{
    "operation": {
        "operation_type": "UPDATE_MAINTENANCE"
    },
    "merchant": {
        "merchant_reference": "30083001"
    },
    "maintenance": {
        "maintenance_reference": "MC3000000001",
        "outlets": [
            {
                "internal_mid": "8001000000100001",
                "reserve": {
                    "reserve_type": 1,
                    "reserve_setting": 1,
                    "reserve_daily_amount": 5,
                    "reserve_trans_perc": 10,
                    "set_reserve_target": 1,
                    "reserve_target_amount": 500
                }
            }
        ]
    }
}
```

| Field Name              | Data Type | Description                                                                                                                                    |
|-------------------------|-----------|------------------------------------------------------------------------------------------------------------------------------------------------|
| `reserve_type`            | Integer   | Type of reserve being configured. 1 - Normal, 2 - Rolling.                                                                                     |
| `reserve_setting`         | Integer   | Reserve collection setting. 1 - Percentage, 2 - Base.                                                                                          |
| `reserve_daily_amount`    | Integer   | Amount to be collected daily. Used for reserve_setting = 2 (Base), specifies the daily amount taken into reserve for the sub-merchant.         |
| `reserve_trans_perc`      | Integer   | Used for reserve_setting = 1 (Percentage). Specifies the percentage taken out of the transactions for the sub-merchant.                        |
| `set_reserve_target`      | Integer   | Flag indicating whether to set a reserve target (1 for true, 0 for false). Will enable reserve_target_amount to be set for the sub-merchant.   |
| `reserve_target_amount`   | Integer   | Maximum amount to collect for the sub-merchant when set_reserve_target is true.                                                                 |
| `reserve_delay_days`      | Integer   | Used for reserve_type = 2 (Rolling). Sets the period of time for the rolling reserve to release amounts. Max 90.                                        |


### Submitting the Case

<!-- theme: info -->
>**POST** `/maintenance`

Once the case has been updated with the settings for the Reserve, it must be submitted using the `maintenance_reference`.
Once submitted, a `"maintenance_status"`: "Completed" means the maintenance is complete, and the reserve settings have been updated.

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

