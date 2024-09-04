
---
tags: [Getting Started, Maintenance, Reserves]
---
# Reserve Maintenance

Reserves can be added to sub-merchants to collect and managed amounts for collateral through Exchange. A Reserve can also be removed, but will require the user to instruct what will happen with any currently held funds. Any currently held funds in Reserve will either need to be released prior to the maintenance case or during the maintenance case (Released to Sub-Merchant or Aggregator).  

## Removing an existing Reserve

### Creating the case

<!-- theme: info -->
>**POST** `/maintenance`

To remove a reserve from an existing sub-merchant, the `REMOVE_RESERVE` maintenance type must be used on the create  

This returns a `maintenance_reference`, unique to this case which can then be updated. The currently held Reserve amount is returned when creating the case, which will be used in the Update step.

### Updating the case

Once created, the case must be updated.
Any amount held in the Reserve must be instructed to be released, or deducted in the maintenance case. `remove_reserve_flag` must be `1` when removing reserve from a node. 

```json
{
    "operation": {
        "operation_type": "UPDATE_MAINTENANCE"
    },
    "merchant": {
        "merchant_reference": "30010001"
    },
    "maintenance": {
        "maintenance_reference": "MC3000000001",
        "merchant": {
            "internal_mid": "100010000001",
            "reserve": {
                "remove_reserve_flag": 1,
                "release_amount": 10,
                "deduct_amount": 5
            }
        }
    }
}

```

| Field Name           | Data Type | Description                                                                                                                                                                                                        |
|----------------------|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `remove_reserve_flag` | Integer   | Flag indicating if reserve should be removed. 1 - Yes 2 - No                                                                                                                                                    |
| `release_amount`     | Number   | Amount of currently held reserve that will be released and settled to the sub-merchant after the case is complete. `release_amount` + `deduct_amount` must equal the amount currently held in reserve. Must be positive            |
| `deduct_amount`      | Number   | Amount of currently held reserve that will be deducted and settled to the Aggregator after the case is submitted. `release_amount` + `deduct_amount` must equal the amount currently held in reserve. Must be positive      |


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

