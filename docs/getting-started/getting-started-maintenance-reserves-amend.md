
---
tags: [Getting Started, Maintenance]
---

# Reserve Maintenance

Reserves can be added to sub-merchants to collect and managed amounts for collateral through Exchange. For Auto-Funding, this can be used to setup a reserve to collect automatically based on settings. For Instructional funding, reserves can be enabled and collected with funding instructions.
Only one maintenance case for reserves on a sub-merchant can be created at a time.
## Amending a Reserve

Reserve settings can be amended for an existing sub-merchant. This can be used to update how the reserve collects for Auto-Funding. 

### Creating the case

<!-- theme: info -->
>**POST** `/maintenance`

The `AMEND_RESERVE` maintenance type must be used, and `merchant_reference` must be provided to create the case.

This returns a `maintenance_reference`, unique to this case which can then be updated.

### Updating the Amend Reserve case

<!-- theme: info -->
>**POST** `/maintenance`

Using the `maintenance_reference`, the case can then be updated. The new settings can be provided. The amended case must be updated same level as the original reserve, so if it was previously set on the "Merchant",
 
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
        "merchant": {
            "internal_mid": "8001000000100001",
            "reserve": {
                "take_reserves_flag": 1,
                "reserve_type": 1,
                "reserve_setting": 1,
                "reserve_daily_amount": 5,
                "reserve_trans_perc": 10,
                "set_reserve_target": 1,
                "reserve_target_amount": 500,
            }
        }
    }
}
```

### Submitting the Case

<!-- theme: info -->
>**POST** `/boarding/outlet/update`



