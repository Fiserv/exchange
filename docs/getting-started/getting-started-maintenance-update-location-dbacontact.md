
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
        "merchant_reference": "5001001"
    },
    "maintenance": {
        "maintenance_reference": "MC5000001001",
        "outlets": [
            {
                "internal_mid": "326023000001",
                "contacts": [
                    {
                        "_id": "ad42966777630006671f6bcd",
                        "contact_type": "OT",
                        "contact_first_name": "Billy",
                        "contact_last_name": "Shears",
                        "country_code": "840",
                        "city": "New York",
                        "zip_code": "10001",
                        "street_line_1": "Broadway",
                        "county_code": "NY",
                        "email_address": "example@fiserv.com",
                        "ent_telephone_code": "US|1",
                        "telephone_number": "3339898989"
                    }
                ]
            }
        ]
    }
}
```

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

