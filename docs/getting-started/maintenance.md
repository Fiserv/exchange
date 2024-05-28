# Merchant Maintenance

## What is Merchant Maintenance?

When using exchange, you may want to update submerchant data or pricing after it has been boarded. In order to do this, a maintenance case must be created.

## General Maintenance process

The user will be able to create a merchant maintenance case with the type of maintenance they would like to do, have this updated, and then submit the case.
This is primarily be facilitated through the `/maintenance` endpoint.

### Creating Maintenance Case

In order to create maintenance case, `/maintenance` endpoint must be used with operation_type : `CREATE_MAINTENANCE`. The user will need to provide the type of maintenance being performed, and the `merchant_reference` for the submerchant. 
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
### Updating Maintenance Case

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
  "maintenance": {
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
}
```
### Submitting the Maintenance Case

Once this has been updated, we can now submit the case using the Maintenance reference number that was returned in the original Create Maintenance call. If succesful, merchant has now been updated with the new details.
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
## Additional Outlet process

### Creating a new outlet

The process for adding an additional outlet is similar to a maintenance case. The user must start by creating an additional outlet to add to an existing merchant by creating a maintenance type with type "ADD_OUTLETS"

This creates an application to add the additional outlet, and returns an `application_reference` which can be updated.

### Adding the new outlet

Adding the outlet to this application is the same as adding the original outlet to an application, and uses the `/boarding/outlet/add` endpoint. The application reference required to be used is returned when creating the maintenance case, and the user should specify the `parent_mid` of the outlet like the standard boarding process. Typically, this will use the internal MID subgroup of the application that can be retrieved.

### Updating the new outlet

The additional outlet can then be updated using the `/boarding/outlet/update` endpoint in order to update the application

### Submitting the new outlet

As this is an application for the outlet, the outlet must be submit using the `/boarding/application` [endpoint](../api/?type=post&path=/boarding//application) for submitting an application.

Just like a normal application, if `submit_success` in the response is `1`, the application succesfully submit to the new step in workflow. Checking the status of the application will allow you to verify if this was succesfully boarded. Once boarded, will be added to the existing merchant.
