---
tags: [Getting Started, Maintenance]
---
# Merchant Maintenance

##  Maintenance Process

The user will be able to create a maintenance case with the type of maintenance they would like to do, have this updated, and then submit the case.
This is primarily be facilitated through the `/maintenance` endpoint.

### Creating Maintenance Cases

<!-- theme: info -->
>**POST** `/maintenance`

In order to create maintenance case, `/maintenance` endpoint must be used with operation_type : `CREATE_MAINTENANCE`. The user will need to provide the type of maintenance being performed, and the `merchant_reference` for the sub-merchant. 
The `old_details` will provide the data being updated, which can be used in the next endpoint to update.
`merchant_reference` can be found by retrieving the merchant using the `boarding/merchant` [endpoint](../api/?type=post&path=/boarding/////merchant)

Example request body:
```
{
  "operation": {
    "operation_type": "CREATE_MAINTENANCE"
  },
  "merchant": {
    "merchant_reference": "3001001"
  },
  "maintenance": {
    "maintenance_types": ["CHANGE_BANK"]
  }
}
```
### Updating Maintenance Cases

<!-- theme: info -->
>**POST** `/maintenance`

Next, the maintenance case must be updated with the new information. Using the `old_details` from the Create maintenance case response, we can use this as a base to populate the new details to be updated.
Depending on the maintenance case, you will need to include the new details in their respective block in the request. ie, banks for Bank changes. Please see [examples](../api/?type=post&path=//maintenance) on the request page for more info

Example for bank change below:
```
{
    "operation": {
        "operation_type": "UPDATE_MAINTENANCE"
    },
    "merchant": {
        "merchant_reference": "30083993"
    },
    "maintenance": [
        {
            "outlets": {
                "maintenance_reference": "MC3000000601",
                "internal_mid": "7001000000500001",
                "banks": [
                    {
                        "_id": "12b5534faf9baf2232bb23c",
                        "bank_name": "Bank of Test",
                        "country_code": "840",
                        "zip_code": "12345",
                        "county_code": "CA",
                        "account_holder_name": "Jane Doe",
                        "bank_account_type": "CHECKING",
                        "dda_number": "123456789",
                        "routing_number": "333456789",
                        "account_type": [
                            "CREDIT",
                            "DEBIT",
                            "CHARGEBACK"
                        ]
                    }
                ]
            }
        }
    ]
}
```
### Submitting the Maintenance Case

<!-- theme: info -->
>**POST** `/maintenance`

Once this has been updated, we can now submit the case using the Maintenance reference number that was returned in the original Create Maintenance call. If successful, the sub-merchant has now been updated with the new details.
```
{
  "operation": {
    "operation_type": "SUBMIT_MAINTENANCE"
  },
  "maintenance": {
    "maintenance_reference": "MC3000000601"
  }
}

```

