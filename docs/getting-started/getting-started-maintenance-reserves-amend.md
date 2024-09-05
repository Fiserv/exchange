
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


