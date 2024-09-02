---
tags: [Getting Started, Maintenance]
---
# Reserve Maintenance

Reserves can be added to submerchants to collect amounts for collateral. This can be used to setup a reserve so that these are collected automatically, for Auto-Funding, or setup to enable reserves to be collected with Instructional Funding using funding instructions.

## Adding a Reserve

To add a reserve to an existing sub-merchant, the `ADD_RESERVE` maintenance type must be used on the create maintenance case endpoint.

### Creating the case

<!-- theme: info -->
>**POST** `/maintenance`

To add a reserve to an existing sub-merchant, the `ADD_RESERVE` maintenance type must be used on the create  

This returns a `maintenance_reference`, unique to this case which can then be updated.

### Updating the Add Reserve case

<!-- theme: info -->
>**POST** `/maintenance`

Adding the location (outlet) to the sub-merchant is the same as adding the original location (outlet) to an application, and uses the `/boarding/outlet/add` endpoint. The application reference required to be used is returned when creating the maintenance case, and the user should specify the `parent_mid` of the location (outlet) like the standard boarding process. Typically, this will be the subgroup of the application.

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
                "reserve_delay_days": 6
            }
        }
    }
}
```

### Updating the New Location

<!-- theme: info -->
>**POST** `/boarding/outlet/update`


If you need to update the location (outlet) information after you added it (but before submission), the location (outlet) can then be updated using the `/boarding/outlet/update` like the standard process.

### Submitting the New Location

## Removing an existing Reserve

### Updating the Remove reserve case

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

