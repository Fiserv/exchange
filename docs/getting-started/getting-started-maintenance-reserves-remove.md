
---
tags: [Getting Started, Maintenance, Reserves]
---
# Reserve Maintenance

Reserves can be added to sub-merchants to collect and managed amounts for collateral through Exchange. For Auto-Funding, this can be used to setup a reserve to collect automatically based on settings. For Instructional funding, reserves can be enabled and collected with funding instructions.
Only one maintenance case for reserves on a sub-merchant can be created at a time.
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
