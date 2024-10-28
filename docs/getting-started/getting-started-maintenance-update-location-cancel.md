
---
tags: [Getting Started, Maintenance, Location]
---

#  Cancel Location Maintenance

Locations can be cancelled through exchange through a maintenance case. This will submit to downstream systems for the location to be cancelled.

## Cancel a location

To cancel an existing sub-merchant, a Maintenance case must be created, updated and submitted. 

### Creating the case

<!-- theme: info -->
>**POST** `/maintenance`

The`CANCEL_LOCATION` maintenance type must be used, and `merchant_reference` must be provided to create the case.

This returns a `maintenance_reference`, unique to this case which can then be updated.

### Updating the Cancel Maintenance case

<!-- theme: info -->
>**POST** `/maintenance`

The reserve settings must be added on the funding/billing level of the sub-merchant. This will usually be at the location (outlet) level, but can also be on the Merchant or chain (subgroup).  The settings you want to set the reserve up with will need to be provided, and the system will start collecting amounts at the next available cycle after the case is completed. 

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

Once the case has been updated with the settings for the Reserve, it must be submitted using the `maintenance_reference`.
Once submitted, a `"maintenance_status"`: "Completed" means the maintenance is complete, and the reserve has been added.

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

Once the case has been updated with the settings for the Reserve, it must be submitted using the `maintenance_reference`.
Once submitted, a `"maintenance_status"`: "Completed" means the maintenance is complete, and the reserve has been added.

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

#### `maintenance_status` Responses

| Responses                                 | Data Type | Description                                                                                                                                                   |
|-------------------------------------------|-----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `Awaiting Maintenance Marketplace Boarding` | String    | Initial transient status for submission downstream.                                                                                                            |
| `Awaiting Maintenance Marketplace Response` | String    | Maintenance details submitted downstream and confirmation received. Adds `orderId` into `maintenance_details`.                                                  |
| `Completed`                               | String    | Maintenance case has been completed and synced.                                                                                                                |
| `Partially Applied`                       | String    | Applicable for maintenance cases with multiple `maintenance_types`. If the case is canceled before downstream sync completes, it is marked as partially applied. |
                                                                    |
