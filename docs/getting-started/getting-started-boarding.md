---
tags: [Getting Started, Boarding, Application]
---


# Boarding APIs

Exchange allows the creation of applications on the system by using a set of boarding APIs. This is comprised of adding the Registered Legal Business Entity, and DBA locations (Outlets)
Once an application is added, it can be submitted to move into downstream systems, and once complete will return with the status 'Boarding Complete'. The flow of an application may differ depending on what services on the system are being utilized.

---

## Adding an application

The standard sub-merchant hierarchy is built from a Merchant, a Chain and a location (outlet). These are sent using the `boarding/add_application` and `outlet/add` endpoints. The chain is added inside the add_application as a subgroup, and is used for structure. Outlets are added to a subgroup.

![boarding_flow](/assets/images/boarding_flow.png)

The basic API flow is as shown in diagram here:

![boarding API](/assets/images/boarding_diagram_v2_resized.png)


### Adding the Merchant and Chain

<!-- theme: info -->
>**POST** `/boarding/add_application`

<!--
type: tab
titles: Add Application, Sample JSON
-->

The `/boarding/add_application` endpoint supports adding the merchant and chain level in one request. This will require legal information to be sent, principal/owner information to be sent, and any application settings to be submitted. An offer can be added at the business level, but typically is done at the outlet level as is in this example. 


<!-- type: tab -->

JSON format for `ADD_APPLICATION`:

```json
{
  "merchant": {
    "business_entity": {
      "legal_name": "MMISTEST Legal Name",
      "ownership_entity_type": "L",
      "foreign_entity": "0",
      "irs_filing_name": "MMISTEST IRS Name",
      "irs_status": "N",
      "tin_type": "2",
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
        "owner_nationality": "840",
        "owner_position": "CEO",
        "owner_phone_code": "US|1",
        "owner_phone_no": "3339898989",
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
    "merchant_sub_group": {
      "group_name": "Subgroup"
    }
  }
}


```

<!-- type: tab-end -->

### Adding Locations (Outlets)

<!-- theme: info -->
>**POST** `/boarding/outlet/add`

<!--
type: tab
titles: Add Location (Outlet) , Sample JSON
-->

The `/boarding/outlet/add` endpoint supports adding the location (outlet) to an application. This will require the Application Reference and Parent MID to be included in the request to link the Location to the application. This is returned in the response to the`ADD_APPLICATION` request, and the parent MID will be the `internal_mid` of the merchant application's subgroup. 
The location (outlet) will contain the Offer, which is used to select which products and entitlements are going to be onboarded with the sub-merchant. Details for retrieving information from the offer can be retrieved using the `product_offer/list` and  `product_offer/retrieve` endpoints. For additional info on these endpoints and data seen here, please see the [Offerings page](?path=docs/getting-started/v4-offerings.md)

<!-- type: tab -->

JSON format for `ADD_OUTLET`:

```json
{
  "application": {
    "application_reference": "333000050001"
  },
  "outlet": {
    "parent_mid": "700100000050001",
    "trade_name": "MMISTest Business Name",
    "outlet_website": "https://fiserv.com",
    "currencies": "USD",
    "business_category": "E",
    "visitation_required": "1",
    "primary_email_address": "email@domain.com",
    "mcc_code": "5733",
    "discover_required": "1",
    "amex_required": "1",
    "amex_volume": "2000.00",
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
    "annual_turnover": "100000.00",
    "annual_card_turnover": "90000.00",
    "average_delivery_days": "1",
    "delivery_0_days_perc": "100",
    "delivery_1_to_7_days_perc": "0",
    "delivery_8_to_14_days_perc": "0",
    "delivery_15_to_30_days_perc": "0",
    "delivery_over_30_days_perc": "0",
    "prod_serv_sold": "Product and services sold",
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
        "routing_number": "333456789",
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
        "telephone_number": "3339898989",
        "email_address": "email@domain.com"
      },
      {
        "contact_type": "B",
        "country_code": "840",
        "city": "Sparks",
        "bill_to": "Jane",
        "contact_first_name": "Jane ",
        "contact_last_name": "Doe",
        "zip_code": "89431",
        "street_line_1": "Sheila Lane",
        "county_code": "NV",
        "ent_telephone_code": "US|1",
        "telephone_number": "3339898989",
        "email_address": "email@domain.com"
      }
    ],
    "offer": {
      "product_offer_code": "PRO00000000001",
      "product_items": [
        {
          "product_code": "GTWY01",
          "quantity": "1"
        }
      ],
      "entitlements": [
        {
          "entitlement_key": "VISA"
        },
        {
          "entitlement_key": "MASTERCARD"
        }
      ]
    }
  }
}

```

<!-- type: tab-end -->


### Submitting an Application

<!-- theme: info -->
>**POST** `/boarding/application`

<!--
type: tab
titles: Application Submit, Sample JSON
-->

The `/boarding/application` endpoint supports submitting the application using the application reference. This requires the operation type `APPLICATION_SUBMIT` to be added to the request. Please see adjacent example for this. Any validation errors will return a `success:` `0` , with the errors detailed in the bottom of the response including what needs to be updated and where. This would require the application to be updated, and resubmitted until it passes the validation. For full specs on this please see the [API Explorer](../api/?type=post&path=/boarding//application).

#### DDA  Verification

If DDA verification is enabled, this will be done upon submission of the application. If successful, the application will submit as normal, with updated `"dda_validated":` `"1"` for the bank details.  
If unsuccessful, the service will provide a response on why. 

| Status                          | Description                                              |
|---------------------------------|----------------------------------------------------------|
| VERIFIED                        | ABA/DDA found and matches PII sent                       |
| PARTIAL                         | ABA/DDA found and partially matches PII sent             |
| NON PARTICIPANT                 | ABA not found in National Shared Database                |
| PARTICIPANT ACCOUNT NOT LOCATED | ABA participates, but DDA cannot be found                |
| NOT VERIFIED                    | ABA/DDA found but does not match PII sent                |

If you want to ignore the DDA service, as you have verified details another way, the  `ignore_bank_validation":` `"1"` flag can be added to the application submission payload.

#### TIN Verification

If TIN verification is enabled, this will be done upon submission of the application.
Flag `tin_validated:` `1` will be updated on the application + merchants details, and indicates it was successful. Unsuccessful validation will result in errors being thrown upon submission, giving any detail on possible matches if available.  
Responses include:

| Result                               | Check Type and Data Points                           | Action                                    |
|--------------------------------------|------------------------------------------------------|-------------------------------------------|
| Possible match found                 | Business TIN, Outlet Trading Name and Outlet Address | Update the business data and retry        |
| Possible match found                 | Business TIN, Business Legal Name and Business Address | Update the business data and retry      |
| Possible match found - Sole Prop     | Principal SSN, Principal Name and Principal Address  | Update the business data and retry        |
| Possible match found - Sole Prop     | Business SSN, Outlet Trading Name and Outlet Address | Update the business data and retry        |
| Possible match found - Sole Prop     | Business EIN, Outlet Trading Name and Outlet Address | Update the business data and retry        |
| No match found                       | N/A                                                  | Update the business data and retry        |

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

### Submission Error Handling 

A set of Validation is done upon using the submission endpoint. This can mean that there are validation checks that may fail. These are reported in the `"errors"`  block.  Submission errors will return with a message, on a description of the error, and context on where this field is found. This typically flags when invalid data entered, or a field not provided.

```json
    {
      "error_code": 1501001,
      "message": "Outlet 1: Trading Information is invalid - The field Annual Card Turnover is required",
      "context": "{\"outlet\":1,\"trading_information\":1}"
    }
```

### Checking application status

The application status check can be used to check current status of application. This will give information on the flow of the application. An application is considered complete once it has reached status 'Boarding Complete'. 
This will also give you information on what credit risk state the application using the `"aml_process_state"`, `"aml_error"`, `"credit_risk_process_state"`, `"CREDIT_RISK_CHECK_ERROR"`. These report the current state, and any potential errors from the risk services.
For example payloads, please see [API explorer](../api?type=post&path=/boarding///application)

#### Error handling 

Upon submission to services in the system, it is possible to receive errors downstream if the data submitted is invalid, or for other system errors.  These are reported in a set of fields in the status API 

## Updating an application

While an Application is in 'Open' status, it can be updated using the UPDATE requests, this can be done for each level of the sub-merchant. 
An applications status and information can be retrieved using the `APPLICATION_STATUS_CHECK` and `RETRIEVE_APPLICATION` requests, and the application can be submitted by using the `APPLICATION_SUBMIT` request (pending validation). Any validation errors will return a success : 0 , with the errors detailed in the bottom of the response, including what needs to be updated and where. This would require the application to be updated and resubmitted until it passes the validation. For full specs on this please see the [API Explorer](../api/?type=post&path=/boarding//application).

### Application Update Requests

<!-- theme: info -->
>**POST** `/boarding/application`

<!--
type: tab
titles: Update Merchant, Sample JSON
-->

The `/boarding/merchant` endpoint supports updating for the merchant level and subgroup level, while the `/boarding/outlet` allows the location (outlet) to be updated.
To update the locations (outlets) and subgroups , the `outlet_external_id` or `sub_group_external_id` must also be added to the request to specify the outlet/sub group, which can be found using the `RETRIEVE_MERCHANT_HIERARCHY` operation at the `/boarding/application` endpoint (see [API specs for this request](../api?type=post&path=/v1/apis)).
The application reference must be added to the request, and operation type based on the update being made.

- UPDATE_MERCHANT at `/boarding/update_merchant` for merchant level.
- UPDATE_MERCHANT_SUB_GROUP at `/boarding/subgroup/update` for subgroup level.
- UPDATE_OUTLET at `/boarding/outlet/update` for location (outlet) level.


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

<!-- theme: info -->
>**POST** `/fdapplication/upload_additional_files`

Files can be uploaded to the application for record keeping purposes. To upload a document to an application, the `/fdapplication/upload_additional_files` endpoint should be used and will require the payload to be sent as form-data. 
The form will require two keys, `request` and `file` - where the request is the body and file is an uploaded file. Only one file at a time can be sent through the API.

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

