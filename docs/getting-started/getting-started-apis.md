---
tags: [Getting Started, API Keys, Environments]
---

# Using our APIs

Exchange uses RESTful APIs to allow requests to be sent to our services, allowing onboarding, reporting, funding and more. These are constructed using a Header and request Body. All APIs on Exchange utilise method POST.

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

```python
import requests

url = "https://uat-api.carat-platforms.fiserv.com/boarding/add_application"
headers = {
    "X-API-VERSION": "3",
    "Content-Type": "application/json",
    "Authorization": "Authorization"
}
payload = {
{
    "limit": 5,
    "page": 1,
    "query": {
        "location_id": {
            "operator": "EQ",
            "value": "52606609801"
        },
        "date_added": {
            "operator": "EQ",
            "value": "2022-01-01"
        }
    }
}
```
<!-- type: tab-end -->


