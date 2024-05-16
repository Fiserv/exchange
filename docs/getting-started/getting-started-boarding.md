---
tags: [Getting Started, Boarding, Application]
---

# Boarding APIs

Exchange allows the creation of applications on the system by using a set of boarding APIs. This is comprised of adding the Registered Legal Business Entity, a Chain (or Subgroup), and DBA locations (Outlets)
Once an application is added, it can be submit to move into downstream systems, and once complete will return with the status 'Boarding complete'. The flow of an application may differ depending on what services on the system are being utlilized.

---

## Adding an application

The standard submerchant hierarchy is built from a Merchant, Chain and an outlet. These are sent using the `boarding/add_application` and `outlet/add` endpoints. 

<!-- !align: center -->
![boarding_flow](/assets/images/boarding_flow.png)

<center>
  <img src="./assets/images/boarding_flow.png" alt="boarding_flow" style="max-width: 50%;" width="500">

</center>


### Adding the Merchant and Chain

<!--
type: tab
titles: Add Application, JSON Add Application Example
-->

The `/boarding/add_application` endpoint supports adding the merchant and chain level in one request. This will require legal information to be sent, principal information , application settings and an offer package if used for adding processing offerings or equipement offerings.


<!-- type: tab -->

JSON format for `ADD_APPLICATION`:

```json
    
{
  "merchant": {
    "business_entity": {
      "legal_name": "MMISTEST Business Name",
      "ownership_entity_type": "L",
      "foreign_entity": "0",
      "irs_filing_name": "MMISTEST Business Name",
      "irs_status": "N",
      "tin_type": "2",
      "int_tax_exempt_flag": "1",
      "business_tin_ssn_number": "666989898",
      "mcc_code": "5733",
      "business_category": "E",
      "foundation_date": "2020-01-01",
      "date_incorporated": "2020-01-01",
      "incorp_state": "CA"
    },
    "owners": [
      {
        "owner_first_name": "Jane",
        "owner_surname": "Doe",
        "contact_dob": "1980-01-01",
        "owner_nationality": "826",
        "owner_position": "CEO",
        "owner_phone_code": "US|1",
        "owner_phone_no": "666989898",
        "owner_date_started": "2020-03-31",
        "owner_email": "email@domain.com",
        "owner_tin_ssn_number": "666989898",
        "is_main_principal": "1",
        "ownership_perc": "100",
        "contacts": [
          {
            "zip_code": "12345",
            "street_line_1": "Sample street 1",
            "city": "Sample City",
            "county_code": "CA",
            "country_code": "840"
          }
        ]
      }
    ],
    "registration_address": {
      "zip_code": "12345",
      "street_line_1": "Sample street 1",
      "city": "Sample City",
      "county_code": "CA",
      "country_code": "840"
    },
    "offer_package": {
      "package_external_id": "OPK01-AB8823-0F2E9-8823J-CC924-C7D40-BCB28"
    },
    "acquiring_offer": {
      "package_external_id": "TP123-8823J-A5ABB-AB8823-65923-34A33-BCB28"
    },
    "merchant_sub_group": {
      "group_name": "Subgroup Name"
    }
  }
}

```

<!-- type: tab-end -->

The offer package and acquiring offer can be set to default using the config portal, and can be removed from the payload if this is being used. If wanting to specify specific items in the offer pacakge or pricing, this will need to be sent seperately. Sending just the external ids will pull all mandatory information.
If specifying the Offer Package and acquiring offers, please use the `/offering/available` and  `/offering/retrieve_processing_offering` endpoints. For additional info on these endpoints and data seen here, please see the [Offerings page](?path=docs/getting-started/offerings.md)

### Adding Outlets

<!--
type: tab
titles: Add Outlet, JSON Add Outlet Example
-->

The `/boarding/outlet/add` endpoint supports adding the outlet to an application, and will require the application reference and the parent MID of where the outlet should be added to be added to the request. This will be retrieved from the `ADD_APPLICATION` request, and the parent MID will be the `internal_mid` of the merchant applications subgroup (as to add for the standard merchant-chain-outlet hierarchy). 


<!-- type: tab -->

JSON format for `ADD_OUTLET`:

```json

{
  "application": {
    "application_reference": "333000050001"
  },
  "outlet": {
    "parent_mid": "700100000050001",
    "trade_name": "MMISTest Bussines Name",
    "outlet_website": "https://fiserv.com",
    "currencies": "USD",
    "visitation_required": "1",
    "primary_email_address": "email@domain.com",
    "mcc_code": "5733",
    "mastercard_sales": "100000.00",
    "visa_sales": "100000.00",
    "visa_mastercard_sales": "100000.00",
    "discover_required": "1",
    "amex_required": "1",
    "amex_volume": "100000.00",
    "turnover_bus_to_bus_perc": "0",
    "turnover_bus_to_cons_perc": "100",
    "card_bus_to_bus_perc": "0",
    "card_bus_to_cons_perc": "100",
    "highest_ticket_sales_amt": "1000.00",
    "sales_ftf_perc": "0",
    "sales_keyed_perc": "100",
    "sales_phone_perc": "0",
    "sales_mail_perc": "0",
    "sales_internet_perc": "100",
    "sales_tradeshow_perc": "0",
    "chip_flag": "Y",
    "annual_turnover": "100000.00",
    "annual_card_turnover": "100000.00",
    "average_delivery_days": "1",
    "delivery_0_days_perc": "100",
    "delivery_1_to_7_days_perc": "0",
    "delivery_8_to_14_days_perc": "0",
    "delivery_15_to_30_days_perc": "0",
    "delivery_over_30_days_perc": "0",
    "prod_serv_sold": "Product and services sold by the submerchant",
    "sales_moto_perc": "10",
    "avg_ticket_sales_amt": "50.00",
    "banks": [
      {
        "bank_name": "Bank of Test",
        "country_code": "840",
        "zip_code": "12345",
        "county_code": "CA",
        "account_holder_name": "Jane Doe",
        "bank_account_type": "CHECKING",
        "dda_number": "123456789",
        "routing_number": "123456789",
        "account_type": [
          "CREDIT",
          "DEBIT",
          "CHARGEBACK"
        ]
      }
    ],
    "contacts": [
      {
        "contact_type": "OT",
        "country_code": "840",
        "city": "Sparks",
        "contact_first_name": "Jane ",
        "contact_last_name": "Doe",
        "zip_code": "89431",
        "street_line_1": "Sheila Lane",
        "county_code": "NV",
        "ent_telephone_code": "US|1",
        "telephone_number": "3334567888",
        "email_address": "email@domain.com"
      }
    ]
  },
  "online_offer": {
    "online_offering_external_id": "EQO01-B4628-962EC-9360F-333CD-5D9D3-072AB"
  }
}

```

<!-- type: tab-end -->


### Submitting an Application

<!--
type: tab
titles: Application Submit, JSON Application Submit Example
-->

The `/boarding/application` endpoint supports submitting the application for the reference parsed. This requires the operation type `APPLICATION_SUBMIT` to be added to the request. Please see adjacent example for this. Any validation errors will return a `success` : 0 , with the errors detailed in the bottom of the response with where they need to be updated. This would require the application to be updated, and resubmit until it passes the validation. For full specs on this please see the  [API explorer](../api?type=post&path=/v1/apis).


<!-- type: tab -->

JSON format for `APPLICATION_SUBMIT`:

```json
{
    "application": {
        "application_reference": "33300XXXXXXXX"
    }
}
```

<!-- type: tab-end -->


## Updating an application

While an Application is in 'Open' status, this can be updated using the UPDATE requests, of which can be done for each level of the sub-merchant. 
An applications status and information can be retrieved using the `APPLICATION_STATUS_CHECK` and `RETRIEVE_APPLICATION` requests, and a complete application can be submit by using the `APPLICATION_SUBMIT` request (pending validation). 
Applications that are invalid will respond with the errors and their locations so that the entity may be updated, and resubmit. 

### Application Update Requests


<!--
type: tab
titles: Update Merchant, JSON Update Merchant Example 
-->

The `/boarding/merchant` endpoint supports updating for the merchant level and subgroup level, while the `/boarding/outlet` allows the outlet to be updated.
To update the outets and subgroups , the `outlet_external_id` or `sub_group_external_id` must also be added to the request to specify the outlet/sub group, which can be found using the `RETRIEVE_MERCHANT_HIERARCHY` operation at the `/boarding/application` endpoint (see [API specs for this request](../api?type=post&path=/v1/apis)).
The application reference must be added to the request, and operation type based on the update being made.

- UPDATE_MERCHANT at `/boarding/update_merchant` for merchant level.
- UPDATE_MERCHANT_SUB_GROUP at `/boarding/subgroup/update` for subgroup level.
- UPDATE_OUTLET at `/boarding/outlet/update` for outlet level.


<!-- type: tab -->

JSON format for `UPDATE_MERCHANT`:

```json
{
    "merchant": {
        "business_entity": {
            "legal_name": "MMISTest 1",
            "ownership_entity_type": "L",
            "application_reference": "33300XXXX"
        }
    }
}
```

<!-- type: tab-end -->

### Uploading Documents to an Application

Files can be uploaded to the application for record keeping purposes.  To upload to an application, the `/fdapplication/upload_additional_files` endpoint should be used and will require the payload to be sent as form-data. 
The form will require two keys, `request` and `file` - where the request is the body and file is an uploaded file. Only one file at a time can be sent through the api

The request must contain the application reference, and the external id of what entity the document is for.
Documents must be configured on the system in order to retrieve the external IDs, and once configured can be retrieved using the `/boarding/document_categories` endpoint.

Example request body:
```
{
    "application": {
        "application_reference": "333020220715",
        "tenant_udc_external_id": "TDC08-23KS2-823JR-72240-34KDF-CAE91-EFB47"
    }
}
```
Please see full specs [Here](../api?type=post&path=/fdapplication/upload_additional_files) for additional details.

