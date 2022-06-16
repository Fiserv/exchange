#  ADD_APPLICATION

## `/boarding/application`

### REQUEST :
```
{
    "request_source": {
        "initiator": "ALLIANCE",
        "alliance_code": "technologi"
        //if "initiator": "PARTNER", "partner_code" will be used
        //if alliance want to add an application for PARTNER, "partner_code" will be used together with "alliance_code"

    },
    "operation": {
        "operation_type": "ADD_APPLICATION",
        "version": "2.0.0"
    },
    "merchant": {
        "business_entity": {
            "legal_name": "technologi",
            "ownership_entity_type": "L",
            "tin_type": "2",
            "business_tin_ssn_number": "333333333",
            "mcc_code": "1111"
        },
        "registration_address": {
            "zip_code": "12345",
            "suite_apart_number": "1",
            "floor": "1",
            "street_line_1": "High Street",
            "city": "City",
            "county_code": "CA",
            "country_code": "840"
        },
        "owners": [
            {
                "owner_title": "Mr.",
                "owner_first_name": "Bailey",
                "owner_second_name": "",
                "owner_surname": "Woods",
                "contact_dob": "1976-01-05",
                "owner_nationality": "826",
                "owner_position": "OW",
                "owner_phone_code" : "US|1",
                "owner_phone_no" : "56747357373",
                "owner_email": "technologi@technologi.co.uk",
                "owner_tin_ssn_number": "123123123",
                "is_main_principal": "1",
                "ownership_perc": "100",
                "contacts": [
                    {
                        "zip_code": "12345",
                        "suite_apart_number": "1",
                        "floor": "1",
                        "street_line_1": "High Street",
                        "city": "City",
                        "county_code": "CA",
                        "country_code": "840"
                    }
                ]
            }
        ],
        "merchant_sub_group": {
            "group_name": "SUB GROUP",
            "same_as_outlet_mid": "1",
            "external_mid": "123456700014",
            "contacts": [
                {
                    "contact_type": "B",
                    "contact_title": "Mr.",
                    "contact_first_name": "John",
                    "contact_second_name": "S",
                    "contact_last_name": "Snow",
                    "floor": "1",
                    "suite_apart_number": "2",
                    "street_number": "",
                    "city": "City",
                    "county_code": "CA",
                    "country_code": "840",
                    "zip_code": "12345",
                    "ent_telephone_code": "US|1",
                    "telephone_number": "07425325869",
                    "email_address": "technologi@technologi.co.uk"
                }
            ], 
            "banks": [
                {
                    "bank_name": "Lloyds",
                    "account_holder_name": "technologi Account1",
                    "bank_account_type": "SAVINGS",
                    "account_type": [
                        "CREDIT"
                    ],
                    "dda_number": "123456789123",
                    "routing_number": "123456789"
                },
                {
                    "bank_name": "Lloyds",
                    "account_holder_name": "technologi Account2",
                    "bank_account_type": "CHECKING",
                    "account_type": [
                        "DEBIT",
                        "CHARGEBACK"
                    ],
                    "dda_number": "46456461234",
                    "routing_number": "123456789"
                }
            ]
        }
    }
}
```

### RESPONSE :
```
{
    "result": "SUCCESS",
    "operation": {
        "operation_type": "ADD_APPLICATION",
        "version": "2.0.0"
    },
    "merchant": {
        "merchant_hierarchy_config_external_id": "MHC44-00000-00000-00000-00000-00000-00000",
        "merchant_hierarchy_template_external_id": "MHTA6-00000-00000-00000-00000-00000-00000",
        "merchant_node_external_id": "MEI36-00000-00000-00000-00000-00000-00000",
        "pfac_node_external_id": "PEIE2-00000-00000-00000-00000-00000-00000",
        "sales_owner_user_external_id": "USR7F-00000-00000-00000-00000-00000-00000",
        "risk_owner_user_external_id": "USR7F-00000-00000-00000-00000-00000-00000",
        "creator_user_external_id": "USR7F-00000-00000-00000-00000-00000-00000",
        "merchant_status_external_id": "OPSC7-00000-00000-00000-00000-00000-00000",
        "alliance_external_id": "ALLCC-00000-00000-00000-00000-00000-00000",
        "application_external_id": "APL73-00000-00000-00000-00000-00000-00000",
        "sales_owner_user_id": "123",
        "merchant_data_id": "60c66eabdddf7a69df000000",
        "parent_type": "ALLIANCE",
        "reserve_entity_level": "2",
        "reserve_type": "1",
        "set_reserve_target": "0",
        "status_id": 1,
        "internal_mid": "700100000007321",
        "billing_frequency": "1",
        "funding_frequency": "1",
        "settlement_method": "1",
        "contact_title": "Mr.",
        "contact_first_name": "Bailey",
        "contact_last_name": "Woods",
        "contact_address1": "High Street",
        "contact_town_city": "City",
        "contact_postcode": "12345",
        "contact_country_code": "840",
        "language_code": "en_gb",
        "date_added": "2021-06-13 20:46:34",
        "date_updated": "2021-06-13 20:46:35",
        "take_reserves_flag": "1",
        "billing_level": "2",
        "funding_level": "2",
        "registration_address": {
            "contact_ref": "60c66eabdddf7a69df000000",
            "country_code": "840",
            "city": "City",
            "zip_code": "12345",
            "street_line_1": "High Street",
            "floor": "1",
            "suite_apart_number": "1"
        },
        "merchant_node_id": "38201",
        "chargeback_settlement_method": "1",
        "business_entity": {
            "legal_name": "technologi",
            "tin_type": "2",
            "business_tin_ssn_number": "333333333",
            "business_tin_ssn_number_masked": "*****3333",
            "business_average_ticket_sales_amt": 0,
            "business_highest_ticket_sales_amt": 0,
            "ownership_entity_type": "L",
            "mcc_code": "1111"
        },
        "owners": [
            {
                "owner_title": "Mr.",
                "owner_first_name": "Bailey",
                "owner_second_name": "",
                "owner_surname": "Woods",
                "contact_dob": "1976-01-05",
                "owner_nationality": "826",
                "owner_position": "OW",
                "is_main_principal": "1",
                "ownership_perc": "100",
                "owner_tin_ssn_number": "123123123",
                "owner_phone_code": "US|1",
                "owner_phone_no": "56747357373",
                "owner_email": "technologi@technologi.co.uk",
                "owner_ref": "60c66eabdddf7a69df0000000",
                "contacts": [
                    {
                        "contact_ref": "60c66eabdddf7a69df0000000",
                        "country_code": "840",
                        "city": "City",
                        "floor": "1",
                        "suite_apart_number": "1",
                        "zip_code": "12345",
                        "street_line_1": "High Street",
                        "county_code": "CA"
                    }
                ]
            }
        ],
        "parent_pfac_node_external_id": "PEIB7-00000-00000-00000-00000-00000-00000",
        "multiple_outlet": "0",
        "application_reference": "333000000000",
        "application_status_external_id": "APSE6-00000-00000-00000-00000-00000-00000",
        "documents": [],
        "funding_settings": {
            "application_reference": "333000000000",
            "settlement_method": "1",
            "chargeback_settlement_method": "1",
            "take_reserves_flag": "1",
            "funding_level": "2",
            "billing_level": "2",
            "reserve_entity_level": "2",
            "funding": {
                "use_default_config_for_all_nodes": "1",
                "configs": [
                    {
                        "entity_key": "DEFAULT",
                        "funding_frequency": "1",
                        "delay_funding_flag": "0"
                    }
                ]
            },
            "billing": {
                "use_default_config_for_all_nodes": "1",
                "configs": [
                    {
                        "entity_key": "DEFAULT",
                        "billing_frequency": "1"
                    }
                ]
            },
            "reserve": {
                "use_default_config_for_all_nodes": "1",
                "configs": [
                    {
                        "entity_key": "DEFAULT",
                        "reserve_type": "1",
                        "set_reserve_target": "0"
                    }
                ]
            }
        }
    },
    "merchant_sub_groups": [
        {
            "sub_group_external_id": "MSG41-00000-00000-00000-00000-00000-00000",
            "pfac_node_external_id": "PEIE2-00000-00000-00000-00000-00000-00000",
            "merchant_node_external_id": "MEI43-00000-00000-00000-00000-00000-00000",
            "merchant_node_id": "38204",
            "sub_group_data_id": "60c66eabdddf7a69df000000",
            "sub_group_type": "CHAIN",
            "parent_mid": "700100000007321",
            "internal_mid": "700100000007322",
            "same_as_outlet_mid": "1",
            "group_name": "SUB GROUP",
            "root_merchant_node_id": "38201",
            "billing_flag": "1",
            "billing_frequency": "1",
            "funding_flag": "1",
            "funding_frequency": "1",
            "reserve_flag": "1",
            "reserve_type": "1",
            "set_reserve_target": "0",
            "delay_funding_flag": "0",
            "hold_suspend_flag": "0",
            "merchant_hierarchy_template_external_id": "MHT50-00000-00000-00000-00000-00000-00000",
            "accounts_setup_flag": "0",
            "banks": [
                {
                    "bank_name": "Lloyds",
                    "bank_account_number": "",
                    "bank_sort_code": "",
                    "iban": "",
                    "swift": "",
                    "account_holder_name": "technologi Account1",
                    "account_type": [
                        "CREDIT"
                    ],
                    "bank_account_type": "SAVINGS",
                    "dda_number": "123456789123",
                    "dda_number_masked": "********9123",
                    "routing_number": "123456789",
                    "routing_number_masked": "*****6789",
                    "_id": "60c66eabdddf7a69df000000"
                },
                {
                    "bank_name": "Lloyds",
                    "bank_account_number": "",
                    "bank_sort_code": "",
                    "iban": "",
                    "swift": "",
                    "account_holder_name": "technologi Account2",
                    "account_type": [
                        "DEBIT",
                        "CHARGEBACK"
                    ],
                    "bank_account_type": "CHECKING",
                    "dda_number": "46456461234",
                    "dda_number_masked": "*******1234",
                    "routing_number": "123456789",
                    "routing_number_masked": "*****6789",
                    "_id": "60c66eabdddf7a69df000000"
                }
            ],
            "contacts": [
                {
                    "contact_type": "B",
                    "contact_title": "Mr.",
                    "contact_first_name": "John",
                    "contact_second_name": "S",
                    "contact_last_name": "Snow",
                    "country_code": "840",
                    "city": "City",
                    "zip_code": "12345",
                    "county_code": "CA",
                    "email_address": "technologi@technologi.co.uk",
                    "ent_telephone_code": "US|1",
                    "telephone_number": "07425325869",
                    "floor": "1",
                    "street_number": "",
                    "suite_apart_number": "2"
                }
            ],
            "external_mid": "123456700014"
        }
    ]
}
```
