
---
tags: [Getting Started, Maintenance]
---
# Reserve Maintenance

Reserves can be added to sub-merchants to collect and managed amounts for collateral through Exchange. For Auto-Funding, this can be used to setup a reserve to collect automatically based on settings. For Instructional funding, reserves can be enabled and collected with funding instructions.
Only one maintenance case for reserves on a sub-merchant can be created at a time.

## Adding a Reserve

To add a reserve to an existing sub-merchant, a Maintenance case must be created, updated and submit. 

### Creating the case

<!-- theme: info -->
>**POST** `/maintenance`

The`ADD_RESERVE` maintenance type must be used, and `merchant_reference` must be provided to create the case.

This returns a `maintenance_reference`, unique to this case which can then be updated.

### Updating the Add Reserve case

<!-- theme: info -->
>**POST** `/maintenance`

The reserve settings must be added on the funding/billing level of the sub-merchant. This will usually be at the outlet level, but can also be on the Merchant or subgroup.  The settings you want to set the reserve up with will need to be provided.
For an auto-funding setup, these will drive how the reserve is collected. 


<!--
type: tab
titles: Auto-Funding Request , Instructional Funding Request
-->

### Auto-Funding Request 

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
                    "take_reserves_flag": 1,
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

### Instructional Funding Request

The reserve settings must be added on the funding/billing level of the sub-merchant. This will usually be at the outlet level, but can also be on the Merchant or subgroup.  The settings you want to set the reserve up with will need to be provided.
For an instructional funding setup, the reserve would need to be enabled only. No settings would be applicable as these are collected by instructions.

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
                    "take_reserves_flag": 1,
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
| `take_reserves_flag`      | Integer   | Flag indicating whether to take reserves (1 for true, 0 for false).                                                                            |
| `reserve_type`            | Integer   | Type of reserve being configured. 1 - Normal, 2 - Rolling.                                                                                     |
| `set_reserve_target`      | Integer   | Flag indicating whether to set a reserve target (1 for true, 0 for false). Will enable `reserve_target_amount` to be set for the sub-merchant.  |
| `reserve_target_amount`   | Integer   | Maximum amount to collect for the sub-merchant when `set_reserve_target` is true.                                                              |
                                                          
---
<!-- type: tab-end -->


### Submitting the Case

<!-- theme: info -->
>**POST** `/maintenance`

Once the case has been updated with the settings for the Reserve, it must be submit using the `maintenance_reference`
Once submit, a `"maintenance_status"`: "Completed" means the maintenance is complete.

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



## Removing an existing Reserve

### Creating the case

<!-- theme: info -->
>**POST** `/maintenance`

To remove a reserve from an existing sub-merchant, the `REMOVE_RESERVE` maintenance type must be used on the create  

This returns a `maintenance_reference`, unique to this case which can then be updated.

### Updating the case

```json
{
    "operation": {
        "operation_type": "UPDATE_MAINTENANCE"
    },
    "merchant": {
        "merchant_reference": "30083993"
    },
    "maintenance": {
        "maintenance_reference": "MC3000000931",
        "merchant": {
            "internal_mid": "20375515",
            "reserve": {
                "remove_reserve_flag": 1,
                "release_deduct_funds": 1,
                "release_amount": 0,
                "deduct_amount": 0
            }
        }
    }
}

```


### Submitting the Case

<!-- theme: info -->
>**POST** `/boarding/outlet/update`