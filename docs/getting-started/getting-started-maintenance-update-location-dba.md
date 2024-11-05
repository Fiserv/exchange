
---
tags: [Getting Started, Maintenance, Boarding, Update Location]
---
# DBA Maintenance

Locations can be cancelled through exchange using a maintenance case. This will submit to downstream systems for the location to be cancelled.

## Updating DBA info

To update DBA info for an existing sub-merchant, a Maintenance case must be created, updated and submit. 
The following fields may  be updated for a location with this case: 

* `primary_email_address`
*  `outlet_website`
*  `trade_name`

### Creating the case

<!-- theme: info -->
>**POST** `/maintenance`

The`CHANGE_DBA` maintenance type must be used, and `merchant_reference` must be provided to create the case.

This returns a `maintenance_reference`, and the `old_details` 


```json
{
    "result": "SUCCESS",
    "operation": {
        "operation_type": "CREATE_MAINTENANCE"
    },
    "maintenance": {
        "maintenance_reference": "MC5000000001",
        "merchant_reference": "5000001",
        "maintenance_status": "Open",
        "has_errors": "0",
        "maintenance_external_id": "MTBCD-C475E-82BE7-B1AA4-9A026-89381-4EA08",
        "creator_user_external_id": "USBCD-C475E-82BE7-B1AA4-9A026-89381-4EA08",
        "status_external_id": "MTS5F-C475E-82BE7-B1AA4-9A026-89381-4EA08",
        "owner_user_external_id": "USABC-C475E-82BE7-B1AA4-9A026-89381-4EA08"
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
        "maintenance_reference": "MC5000000001",
        "merchant_reference": "5000001",
        "maintenance_types": [
            "CHANGE_DBA"
        ],
        "old_details": {
            "outlets": {
                "6c933e018965d93e0147": {
                    "primary_email_address": "testaddress@fiserv.com",
                    "outlet_website": "https://fiserv.com",
                    "trade_name": "MMISTEST Tradename"
                }
            }
        }
    }
}
```

### Updating the DBA Case

<!-- theme: info -->
>**POST** `/maintenance`

<!--
type: tab
titles: Request , Response
-->

### Update Request

The new details must be provided on the outlet for the location being updated. The internal MID must be provided in order to identify the location. 

```json
{
    "operation": {
        "operation_type": "UPDATE_MAINTENANCE"
    },
    "merchant": {
        "merchant_reference": "5000001"
    },
    "maintenance": {
        "maintenance_reference": "MC5000000001",
        "outlets": [
            {
                "internal_mid": "321000071001",
                "primary_email_address": "newemail@fiserv.com",
                "outlet_website": "https://developer.fiserv.com/product/exchange",
                "trade_name": "MMISTEST NewDBA"
            }
        ]
    }
}
```
---


<!-- type: tab -->


### Update Response

A successful update request will provide a response, which contains the old and new details being updated. 
Once updated successfully, can be submit.

```json
{
    "result": "SUCCESS",
    "operation": {
        "operation_type": "UPDATE_MAINTENANCE"
    },
    "maintenance": {
        "maintenance_reference": "MC5000000001",
        "merchant_reference": "5000001",
        "maintenance_status": "Open",
        "has_errors": "0",
        "maintenance_external_id": "MTBCD-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
        "creator_user_external_id": "USBCD-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
        "status_external_id": "MTS5F-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
        "owner_user_external_id": "USABC-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX"
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
        "maintenance_reference": "MC5000000001",
        "merchant_reference": "5000001",
        "maintenance_types": [
            "CHANGE_DBA"
        ],
        "old_details": {
            "outlets": {
                "6c933e018965d93e0147": {
                    "primary_email_address": "testaddress@fiserv.com",
                    "outlet_website": "https://fiserv.com",
                    "trade_name": "MMISTEST Tradename"
                }
            }
        },
        "new_details": {
            "outlets": {
                "6c933e018965d93e0147": {
                "primary_email_address": "newemail@fiserv.com",
                "outlet_website": "https://developer.fiserv.com/product/exchange",
                "trade_name": "MMISTEST NewDBA"
            }
            }
        }
    }
}
```
                                                      
---
<!-- type: tab-end -->


### Submitting the Case

<!-- theme: info -->
>**POST** `/maintenance`

Once the case has been updated with the location details, it must be submit using the `maintenance_reference`.
Once submit, this will begin syncing downstream and will need to be retrieved for updates on completion.

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
            "CHANGE_DBA"
        ],
        "orderId": "xe001",
        "old_details": {
            "outlets": {
                "6c933e018965d93e0147": {
                    "primary_email_address": "testaddress@fiserv.com",
                    "outlet_website": "https://fiserv.com",
                    "trade_name": "MMISTEST Tradename"
                }
            }
        },
        "new_details": {
            "outlets": {
                "6c933e018965d93e0147": {
                    "primary_email_address": "newemail@fiserv.com",
                    "outlet_website": "https://fiserv.com",
                    "trade_name": "MMISTEST NewDBA"
                }
            }
        }
    }
}
```

| `maintenance_status` | Data Type | Description                                                                                                                                    |
|-------------------------|-----------|------------------------------------------------------------------------------------------------------------------------------------------------|
| `Awaiting Maintenance Marketplace Boarding`      | String   |  Initial transient status for submission downstream.                                                                        |
| `Awaiting Maintenance Marketplace Response`      | String   |  Maintenance details submit downstream and confirmation. Adds `orderId` into `maintenance_details`.                                                              |
| `Completed`      | String   |  Maintenance case has completed, and synced.                                                                        |
| `Partially Applied`      | String   |  Only applicable for maintenance cases that have more than `maintenance_types` , which affect a merchant in downstream systems as well as a maintenance type that is only applied within exchange. If the case is cancelled before the dowstream syncs are complete, the case is marked as partially applied.                                                                        |
