
---
tags: [Getting Started, Maintenance, Reserves]
---
# Reserve Maintenance

Reserves can be added to sub-merchants to collect and managed amounts for collateral through Exchange. A reserve can also be removed, but will require the user to instruct what will happen with any currently held funds. These will either need to be release prior to the maintenance case, or instructions specified in the Maintenance case on how much of the reserve should be released back to the sub-merchant, or released to the Aggregator.

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

| Field Name           | Data Type | Description                                                                                                                                                                                                        |
|----------------------|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `remove_reserve_flag` | Integer   | Flag indicating if reserve should be removed. 1 - Yes 2 - No                                                                                                                                                    |
| `release_amount`     | Integer   | Amount of currently held reserve that will be released and settled to the sub-merchant after the case is complete. `release_amount` + `deduct_amount` must equal the amount currently held in reserve.            |
| `deduct_amount`      | Integer   | Amount of currently held reserve that will be deducted and settled to the Aggregator after the case is submitted. `release_amount` + `deduct_amount` must equal the amount currently held in reserve.       |


### Submitting the Case

<!-- theme: info -->
>**POST** `/maintenance`

Once the case has been updated with the settings for the Reserve, it must be submit using the `maintenance_reference`
Once submit, a `"maintenance_status"`: "Completed" means the maintenance is complete and the reserve has been removed.

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

