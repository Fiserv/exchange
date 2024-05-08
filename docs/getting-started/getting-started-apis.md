---
tags: [Getting Started, API Keys, Environments]
---

# Using our APIs

Exchange uses RESTful APIs to allow requests to be sent to our services, allowing onboarding, reporting, funding and more. These are constructed using a Header and request Body. All APIs on Exchange utilise method POST.
---
## Environments

Exchange provides two environments for you to access. UAT / Stage , for testing, and the Production / Live environment.

### UAT
<!-- theme: info -->
> https://uat-api.carat-platforms.fiserv.com/{endpoint}

Pre production environment for testing onboarding, funding, settlement and other APIs being consumed before production.

### Production
<!-- theme: info -->
> https://api.carat-platforms.fiserv.com/{endpoint}

Live environment for onboarding and processing for live locations.
## Exchange Headers

Exchange uses standard Auth + Content type headers, as well as a header to define the version of the API being used. Please see below table for constructing header:

<!--
type: tab
titles: API Headers, Example
-->
| Header | Type | Length | Description |
| -------- | :--: | :------------: | ------------------ |
| `Content-Type` | *string* | N/A |  Content type. Standard request Value (application/json), Document uploads require (multipart/form-data) |
| `X-API-VERSION` | *string* | 1 | Version of the API to be specified. Latest version should be used where applicable. Example: 3 |
| `Authorization` | *string* | N/A | Used to send authentication to the server. Basic Auth where credentials are encrypted in Base64. |

---

<!-- type: tab -->

### Sample Header:

```json
{
  "Content-Type": "application/json",
  "X-API-VERSION": "3",
  "Authorization": "AUTHORIZATION"
}
```

<!-- type: tab-end -->

## API Requests

Depending on the request, the body of the payload will change. Please see below sample of an add_application request.

### Application Request Example

```json
import requests

url = "https://uat-api.carat-platforms.fiserv.com/boarding/add_application"
headers = {
    "X-API-VERSION": "3",
    "Content-Type": "application/json",
    "Authorization": "Authorization"
}
payload = {
    "merchant": {
        "business_entity": {
            "legal_name": "MMISTEST Legal Name",
            "ownership_entity_type": "L",
            "foreign_entity": "0",
            "irs_filing_name": "MMISTEST IRS Name",
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
                "owner_nationality": "840",
                "owner_position": "CEO",
                "owner_phone_code": "US|1",
                "owner_phone_no": "3339898989",
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
            "transaction_pricing_external_id": "TP123-8823J-A5ABB-AB8823-65923-34A33-BCB28"
        },
        "merchant_sub_group": {
            "group_name": "Subgroup"
        }
    }
}
```
<!-- type: tab-end -->



