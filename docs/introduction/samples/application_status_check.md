## `/boarding/application` APPLICATION_STATUS_CHECK
```
REQUEST:
{
  "request_source": {
        "initiator": "ALLIANCE",
        "provider_id": "technologi"
  },
  "operation": {
    "operation_type": " APPLICATION_STATUS_CHECK",
    "version": "2.0.0"
  },
  "application": {
    "application_reference": "333000000000"
  }
}

REQUEST:
{
    "result": "SUCCESS",
    "operation": {
        "operation_type": "APPLICATION_STATUS_CHECK",
        "version": "2.0.0"
    },
    "application": {
        "merchant_node_external_id": "MEI3F-00000-00000-00000-00000-00000-00000",
        "sales_owner_user_external_id": "USR19-00000-00000-00000-00000-00000-00000",
        "risk_owner_user_external_id": "USR19-00000-00000-00000-00000-00000-00000",
        "creator_user_external_id": "USR19-00000-00000-00000-00000-00000-00000",
        "alliance_external_id": "ALL95-00000-00000-00000-00000-00000-00000",
        "internal_mid": "700100000002930",
        "contact_title": "Mr.",
        "contact_first_name": "Bailey",
        "contact_last_name": "Woods",
        "contact_address1": "High Street",
        "contact_town_city": "City",
        "contact_postcode": "12345",
        "contact_country_code": "840",
        "contact_position": "OW",
        "billing_frequency": "1",
        "hold_suspend_flag": "0",
        "funding_frequency": "1",
        "settlement_method": "2",
        "parent_type": "ALLIANCE",
        "reserve_entity_level": "2",
        "reserve_flag": "1",
        "street_line_1": "High Street",
        "city": "City",
        "zip_code": "12345",
        "country_code": "840",
        "language_code": "en_gb",
        "date_added": "2021-06-13 20:59:32",
        "date_updated": "2021-06-13 22:27:03",
        "pfac_node_external_id": "PEID2-00000-00000-00000-00000-00000-00000",
        "status_external_id": "APSE6-00000-00000-00000-00000-00000-00000",
        "application_status_key": "OPEN"
    },
    "errors": [
        {
            "error_code": 1126244,
            "message": "Business Information Address is invalid - Business Registration is required if the Business Type is Limited",
            "date_added": null,
            "date_updated": null
        },
        {
            "error_code": 1126242,
            "message": "Business Information Address is invalid - Credit Bank is required. No credit banks were set on the Funding Level",
            "date_added": null,
            "date_updated": null
        },
        {
            "error_code": 1126241,
            "message": "Business Information Address is invalid - Debit Bank is required. No debit banks were set on the Billing Level",
            "date_added": null,
            "date_updated": null
        },
        {
            "error_code": 1137004,
            "message": "Outlet : Outlet data is invalid - Merchant Settlement Type must be Net Credit for this PFAC",
            "date_added": null,
            "date_updated": null
        },
        {
            "error_code": 1137003,
            "message": "Outlet : Outlet data is invalid - Reserve Target Amount has not been set in Funding Settings",
            "date_added": null,
            "date_updated": null
        },
        {
            "error_code": 1126231,
            "message": "Group %0%: Subgroup data is invalid - Debit Bank is not set on the correct Billing Level",
            "date_added": null,
            "date_updated": null
        },
        {
            "error_code": 1126232,
            "message": "Group %0%: Subgroup data is invalid - Credit Bank is not set on the correct Funding Level",
            "date_added": null,
            "date_updated": null
        }
    ]
}






```
