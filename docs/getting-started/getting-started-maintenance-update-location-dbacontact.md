
---
tags: [Getting Started, Maintenance, Update Location]
---

# DBA Contact Maintenance

Certain DBA contact information can be updated through a maintenance case in Exchange, which will flow through to downstream systems.

## Updating a DBA Contact

The following fields may be updated for a location's DBA contact with this case: 

*  `contact_first_name`
*  `contact_last_name`
*  `country_code`
*  `city`
*  `zip_code`
*  `street_line_1`
*  `county_code`
*  `email_address`
*  `ent_telephone_code`
*  `telephone_number`

### Creating the case

<!-- theme: info -->
>**POST** `/maintenance`

The `CHANGE_DBA_CONTACT` maintenance type must be used, and `merchant_reference` must be provided to create the case.

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
        "325000100001": {
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

Using the `maintenance_reference`, the case can then be updated and the new DBA contact details provided. This will update the main contact for the outlet. 
The `_id` of the contact and `internal_mid` of the location must be provided in the request, and is contained in the the previous create maintenance response. 
The new details can then provided below. `contact_type` also must be provided and should match from the original contact data "OT" currently.
 
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

Once the case has been updated with the new DBA contact details, it must be submitted using the `maintenance_reference`.
Once submitted, this will begin syncing downstream and will need to be retrieved for updates on completion.

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

If the response of the maintenance case returns `"has_errors" : 1` , this means the new submission failed validation. The maintenance_error for this is provided in the `maintenance_errors` array.

Example snippet below: 

```json
...
    "maintenance_errors": [
        {
            "message": "Outlet : Outlet data is invalid - No new details have been submitted"
        }
    ]
...
```


### Retrieving the Case

<!-- theme: info -->
>**POST** `/maintenance`

The maintenance case can be retrieved to review the details, and to check on the `maintenance_status`.
The `"maintenance_status"` shows the current state of the case. 
For cases that sync downstream, we will have additional statuses that show the syncing process before completion and are provided below.
Upon submission, the status will be `Awaiting Maintenance Marketplace Boarding` , and can be expected to move to `Completed` within an hour. 

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
        "325000100001": {
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
| `Partially Applied`      | String   |  Only applicable for maintenance cases that have more than one `maintenance_types` , which affect a location in downstream systems as well as a maintenance type that is only applied within Exchange. If the case is cancelled before the dowstream syncs are complete, the case is marked as partially applied.                                                                        |
