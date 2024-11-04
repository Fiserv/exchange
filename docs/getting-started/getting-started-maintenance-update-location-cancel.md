
---
tags: [Getting Started, Maintenance, Update Location, Cancel Location]
---

#  Cancel Location Maintenance

Locations can be cancelled through exchange using a maintenance case. This will submit to downstream systems for the location to be cancelled.

## Cancel a location

To cancel an existing sub-merchant, a Maintenance case must be created, updated and submitted.
If the sub-merchant is doing billing or funding through the platform, all money must be cleared and the account must first be 'suspended'. Please see the suspend endpoint [here](../api/?type=post&path=/account) 

### Creating the case

<!-- theme: info -->
>**POST** `/maintenance`

The`CANCEL_LOCATION` maintenance type must be used, and `merchant_reference` must be provided to create the case.

This returns a `maintenance_reference`, unique to this case which can then be updated.

### Updating the Cancel Maintenance case

<!-- theme: info -->
>**POST** `/maintenance`

The merchant level internal MID is required to be provided, which can be acquired from the retrieve API or when storing from initial submission. 
The `cancel_location_details` block is then used to specify the location (outlet) that is being cancelled. This will usually be the processing MID of the sub-merchant. 
The `cancellation_reason` must be provided, which allows values 'Cancelled' or 'Cancelled for Fraud'.

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
        "merchant": {
            "internal_mid": "600100000090001"
        },
        "cancel_location_details": {
            "location_to_cancel": "325000100001",
            "cancellation_reason": "Cancelled"
        }
    }
}
```

### Submitting the Case

<!-- theme: info -->
>**POST** `/maintenance`

Once the case has been updated with the location to be cancelled, it must be submit.
Once submit, this will begin syncing downstream and will need to be retrieved for updates on completion.

```json
{
    "operation": {
        "operation_type": "SUBMIT_MAINTENANCE"
    },
    "maintenance": {
        "maintenance_reference": "MC5000001001"
    }
}
```

### Retrieving the Case

<!-- theme: info -->
>**POST** `/maintenance`

The initial `"maintenance_status"` will be `Awaiting Maintenance Marketplace Boarding` , and can be expected to move to `Completed` within an hour. 
The maintenance case can be retrieved to review the details, and to check on the `maintenance_status`.

```json
{
    "result": "SUCCESS",
    "operation": {
        "operation_type": "RETRIEVE_MAINTENANCE"
    },
    "maintenance": {
        "maintenance_reference": "MC5000001001",
        "merchant_reference": "5001001",
        "maintenance_status": "Awaiting Maintenance Marketplace Boarding",
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
        "maintenance_reference": "MC5000001001",
        "merchant_reference": "5001001",
        "maintenance_types": [
            "CANCEL_LOCATION"
        ],
        "cancel_location_details": {
            "location_to_cancel": "325000100001",
            "cancellation_reason": "Cancelled"
        },
        "orderId": "xe001"
    }
}
```

| maintenance_status Responses             | Data Type | Description                                                                                                                                    |
|-------------------------|-----------|------------------------------------------------------------------------------------------------------------------------------------------------|
| `Awaiting Maintenance Marketplace Boarding`      | String   |  Initial transient status for submission downstream.                                                                        |
| `Awaiting Maintenance Marketplace Response`      | String   |  Maintenance details submit downstream and confirmation. Adds `orderId` into `maintenance_details`.                                                              |
| `Completed`      | String   |  Maintenance case has completed, and synced.                                                                        |
| `Partially Applied`      | String   |  Only applicable for maintenance cases that have more than `maintenance_types` , which affect a merchant in downstream systems as well as a maintenance type that is only applied within exchange. If the case is cancelled before the dowstream syncs are complete, the case is marked as partially applied.                                                                        |
