# APPLICATION_SUBMIT

## `/boarding/application` 

### REQUEST:
```
{
  "request_source": {
        "initiator": "ALLIANCE",
        "provider_id": "technologi"
  },
  "operation": {
    "operation_type": "APPLICATION_SUBMIT",
    "version": "2.0.0"
  },
  "application": {
    "application_reference": "333000000000"
  }
}
```
### RESPONSE:
```
{
    "result": "SUCCESS",
    "operation": {
        "operation_type": "APPLICATION_SUBMIT",
        "version": "2.0.0"
    },
    "submit_success": "0",
    //if the submission is successful, "submit_success": "1"

    "application": {
        "application_external_id": "APL6E-56435-D11AF-C0385-78282-3A01D-06F80",
        "sales_owner_user_external_id": "USR19-F03B8-2DCC3-659A8-D685F-260E8-D5826",
        "risk_owner_user_external_id": "USR19-F03B8-2DCC3-659A8-D685F-260E8-D5826",
        "creator_user_external_id": "USR19-F03B8-2DCC3-659A8-D685F-260E8-D5826",
        "alliance_external_id": "ALL95-DB3EE-12B50-3AE7A-A1C65-D25F6-AB746",
        "parent_pfac_node_external_id": "PEIDB-28EEF-B5AC5-0257B-FFFC6-395F5-442E9",
        "multiple_outlet": "0",
        "application_reference": "333000003186",
        "bank_lock": "0",
        "contact_first_name": "Bailey",
        "contact_last_name": "Woods",
        "parent_type": "ALLIANCE",
        "internal_mid": "700100000002930",
        "application_resubmitted": "0",
        "hierarchy_linking_flag": "0",
        "correspondence_language": "en_gb",
        "date_added": "2021-06-13 20:59:32",
        "application_status_external_id": "APSE6-88106-8A5D6-E3F0E-1FBF8-6C93B-95DE4",
        "application_status_key": "OPEN",
        "data_review_required": "0"
    },
    "substatuses": [],
    "alliance": {
        "alliance_external_id": "ALL95-DB3EE-12B50-3AE7A-A1C65-D25F6-AB746",
        "pfac_node_external_id": "PEID2-7D79D-AA7AA-B9D4B-18708-7ACC0-1C624",
        "time_zone_external_id": "TZI34-62EF6-3B32F-C3DB5-654E7-98485-26163",
        "alliance_code": "MOTIONSOFT",
        "alliance_name": "technologi",
        "sales_force_id": "600",
        "portal_access_with_ip": "1",
        "api_access_with_ip": "1",
        "use_memorable_word": "1",
        "client_id": "",
        "client_group_number": "",
        "banker_id": "",
        "institution_number": "006877568",
        "contact_company_name": "PFONE",
        "contact_title": "Dr.",
        "contact_firstname": "fwue",
        "contact_surname": "wgjioe",
        "contact_address1": "Sample Address ",
        "contact_address2": "Sample",
        "contact_town_city": "Sample",
        "contact_county": "Berkshire",
        "contact_postcode": "ABC 322",
        "contact_country": "840",
        "contact_country_name": "United States",
        "contact_phone_code": "US|1",
        "contact_phone": "333548333",
        "contact_mobile_code": "US|1",
        "contact_mobile": "333548333",
        "contact_email": "fiopfjio@test.com",
        "default_currency": "USD",
        "default_language": "en_gb",
        "allowed_alt_languages": "en_gb",
        "time_format": "24",
        "date_format": "mmddyyyy",
        "number_separator": ".",
        "decimal_separator": ",",
        "status": "1",
        "has_own_workflow": "1",
        "date_added": "2019-03-28 15:31:24",
        "pfac_mode": "1",
        "funding_flag": "0",
        "hold_suspend_flag": "0",
        "copied_offer_records_config": "0",
        "underwriting_type": "1"
    },
    "application_relation": {
        "_id": "60c671b4ca31893ef77a44f8",
        "application_id": "4813",
        "application_reference": "333000003186",
        "application_type": null,
        "quote_id": null,
        "price_model": null,
        "business_id": "60c671b4ca31893ef77a44f7",
        "original_merchant_id": null,
        "ownership": null,
        "funding_settings_id": "60c671b4ca31893ef77a44fd",
        "merchant_node_id": "13357",
        "merchant_reference": null,
        "account_settings_id": null,
        "sub_group_id": null,
        "main_owner": "60c671b4ca31893ef77a44f5",
        "main_outlet": "60c676bfd862d7088346f9a3",
        "total_outlets": 1,
        "total_billings": null,
        "total_chains": 0,
        "total_subgroups": 0,
        "aml_check_response": null,
        "credit_risk_decision": null,
        "credit_risk_classification": null,
        "risk_classification": null,
        "intelligence_data_ref": null,
        "intelligence_ref": null,
        "risk_ref": null,
        "aml_ref": null,
        "owner": [
            {
                "owner_id": "60c671b4ca31893ef77a44f5",
                "date_added": null,
                "date_updated": null
            }
        ],
        "submerchants": null,
        "merchant_sub_group": {
            "60c671b4ca31893ef77a44fc": {
                "sub_group_id": "7435",
                "sub_group_data_id": "60c671b4ca31893ef77a44fc",
                "merchant_node_id": "13360",
                "parent_id": null,
                "parent_mid": "700100000002930",
                "internal_mid": "700100000002931",
                "sub_group_type": "CHAIN",
                "date_added": null,
                "date_updated": null
            }
        },
        "chain": null,
        "outlet": {
            "60c676bfd862d7088346f9a3": {
                "outlet_number": 1,
                "crud_outlet_id": null,
                "outlet_auto_id": "4786",
                "merchant_node_id": "13363",
                "outlet_id": "60c676bfd862d7088346f9a3",
                "sub_group_id": "7435",
                "outlet_arrangement_id": null,
                "date_added": null,
                "date_updated": null
            }
        },
        "application": null,
        "date_added": {
            "$date": {
                "$numberLong": "1623617972753"
            }
        },
        "date_updated": {
            "$date": {
                "$numberLong": "1623619263187"
            }
        },
        "total_submerchants": 0
    },
    "business_data": {
        "billing_level": "1",
        "business_entity": {
            "contacts": [],
            "banks": []
        },
        "existing_banks": [],
        "owners": [
            {
                "is_main_principal": "1",
                "owner_title": "Mr.",
                "owner_first_name": "Bailey",
                "owner_second_name": "",
                "owner_surname": "Woods",
                "contact_dob": "1976-01-05",
                "owner_position": "OW",
                "owner_email": "technologi@technologi.co.uk",
                "owner_nationality": "826",
                "ownership_perc": "100",
                "owner_tin_ssn_number": "123123123",
                "_id": "60c671b4ca31893ef77a44f5",
                "contacts": [
                    {
                        "contact_type": "OWM",
                        "_id": "60c671b4ca31893ef77a44f6",
                        "zip_code": "12345",
                        "street_line_1": "High Street",
                        "city": "City",
                        "county_code": "CA",
                        "country_code": "840"
                    }
                ]
            }
        ]
    },
    "errors": [
        {
            "error_code": 1126244,
            "message": "Business Information Address is invalid - Business Registration is required if the Business Type is Limited",
            "context": "{\"business_contact\":\"registration_address\"}"
        },
        {
            "error_code": 1126242,
            "message": "Business Information Address is invalid - Credit Bank is required. No credit banks were set on the Funding Level",
            "context": "{\"business_contact\":\"registration_address\"}"
        },
        {
            "error_code": 1126241,
            "message": "Business Information Address is invalid - Debit Bank is required. No debit banks were set on the Billing Level",
            "context": "{\"business_contact\":\"registration_address\"}"
        },
        {
            "error_code": 1137004,
            "message": "Outlet : Outlet data is invalid - Merchant Settlement Type must be Net Credit for this PFAC",
            "context": "{\"outlet\":null}"
        },
        {
            "error_code": 1137003,
            "message": "Outlet : Outlet data is invalid - Reserve Target Amount has not been set in Funding Settings",
            "context": "{\"outlet\":null}"
        }
    ]
}
```
