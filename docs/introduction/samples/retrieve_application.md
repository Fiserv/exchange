## `/boarding/application` RETRIEVE_APPLICATION
```
REQUEST:
{
  "operation": {
    "operation_type": "RETRIEVE_MERCHANT_HIERARCHY",
    "version": "2.0.0"
  },
  "application": {
    "application_reference": "33300000000"
  }
}

RESPONSE:
{
    "result": "SUCCESS",
    "operation": {
        "operation_type": "RETRIEVE_MERCHANT_HIERARCHY",
        "version": "2.0.0"
    },
    "application_relation": {
        "_id": "60c671b4ca31893ef77a0000",
        "application_id": "4813",
        "application_reference": "33300000000",
        "application_type": null,
        "quote_id": null,
        "price_model": null,
        "business_id": "60c671b4ca31893ef77a0000",
        "original_merchant_id": null,
        "ownership": null,
        "funding_settings_id": "60c671b4ca31893ef77a0000",
        "merchant_node_id": "13357",
        "merchant_reference": null,
        "account_settings_id": null,
        "sub_group_id": null,
        "main_owner": "60c671b4ca31893ef77a0000",
        "main_outlet": "60c671b4ca31893ef77a0000",
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
                "owner_id": "60c671b4ca31893ef77a0000",
                "date_added": null,
                "date_updated": null
            }
        ],
        "submerchants": null,
        "merchant_sub_group": {
            "60c671b4ca31893ef77a0000": {
                "sub_group_id": "7435",
                "sub_group_data_id": "60c671b4ca31893ef77a0000",
                "merchant_node_id": "13360",
                "parent_id": null,
                "parent_mid": "700100000002930",
                "internal_mid": "700100000002931",
                "sub_group_type": "CHAIN",
                "date_added": null,
                "date_updated": null
            }
        },
        "outlet": {
            "60c676bfd862d7088346f9a3": {
                "outlet_number": 1,
                "crud_outlet_id": null,
                "outlet_auto_id": "4786",
                "merchant_node_id": "13363",
                "outlet_id": "60c671b4ca31893ef77a0000",
                "sub_group_id": "7435",
                "outlet_arrangement_id": null,
                "date_added": null,
                "date_updated": null,
                "merchant_node_external_id": "MEI7D-00000-00000-00000-00000-00000-00000"
            }
        },
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
    "alliance": {
        "alliance_external_id": "ALL95-00000-00000-00000-00000-00000-00000",
        "pfac_node_external_id": "PEID2-00000-00000-00000-00000-00000-00000",
        "time_zone_external_id": "TZI34-00000-00000-00000-00000-00000-00000",
        "alliance_code": " technologi",
        "alliance_name": "technologi",
        "sales_force_id": "600",
        "portal_access_with_ip": "1",
        "api_access_with_ip": "1",
        "use_memorable_word": "1",
        "client_id": "",
        "client_group_number": "",
        "banker_id": "",
        "institution_number": "006877568",
        "contact_company_name": "technologi",
        "contact_title": "Dr.",
        "contact_firstname": "technologi",
        "contact_surname": "technologi",
        "contact_address1": "123 Street",
        "contact_address2": "",
        "contact_town_city": "City",
        "contact_county": "CA",
        "contact_postcode": "12345",
        "contact_country": "840",
        "contact_country_name": "United States",
        "contact_phone_code": "US|1",
        "contact_phone": "0905486112",
        "contact_mobile_code": "US|1",
        "contact_mobile": "0945448498",
        "contact_email": "technologi@technologi.co.uk",
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
    "application": {
        "merchant_hierarchy_config_external_id": "MHC47-00000-00000-00000-00000-00000-00000",
        "merchant_hierarchy_template_external_id": "MHT2D-00000-00000-00000-00000-00000-00000",
        "merchant_node_external_id": "MEI3F-00000-00000-00000-00000-00000-00000",
        "pfac_node_external_id": "PEID2-00000-00000-00000-00000-00000-00000",
        "sales_owner_user_external_id": "USR19-00000-00000-00000-00000-00000-00000",
        "risk_owner_user_external_id": "USR19-00000-00000-00000-00000-00000-00000",
        "creator_user_external_id": "USR19-00000-00000-00000-00000-00000-00000",
        "merchant_status_external_id": "OPSC7-00000-00000-00000-00000-00000-00000",
        "alliance_external_id": "ALL95-00000-00000-00000-00000-00000-00000",
        "application_external_id": "APL6E-00000-00000-00000-00000-00000-00000",
        "sales_owner_user_id": "404",
        "merchant_data_id": "60c671b4ca31893ef770000",
        "parent_type": "ALLIANCE",
        "reserve_entity_level": "2",
        "reserve_flag": "1",
        "reserve_type": "1",
        "status_id": "1",
        "internal_mid": "700100000002930",
        "billing_frequency": "1",
        "hold_suspend_flag": "0",
        "funding_frequency": "1",
        "settlement_method": "2",
        "accounts_setup_flag": "0",
        "contact_title": "Mr.",
        "contact_first_name": "Bailey",
        "contact_last_name": "Woods",
        "contact_address1": "High Street",
        "contact_town_city": "City",
        "contact_postcode": "12345",
        "contact_country_code": "840",
        "language_code": "en_gb",
        "date_added": "2021-06-13 20:59:32",
        "date_updated": "2021-06-13 21:21:40",
        "has_validation_errors": "1",
        "take_reserves_flag": "1",
        "billing_level": "1",
        "funding_level": "1",
        "registration_address": {
            "contact_ref": "60c671b4ca31893ef7700000",
            "country_code": "840",
            "city": "City",
            "zip_code": "12345",
            "street_line_1": "High Street",
            "floor": "1",
            "suite_apart_number": "1"
        },
        "merchant_node_id": "13357",
        "chargeback_settlement_method": "1",
        "business_entity": {
            "legal_name": "technologi",
            "tin_type": "2",
            "business_tin_ssn_number": "333333333",
            "business_tin_ssn_number_masked": "*****3333",
            "business_average_ticket_sales_amt": 0,
            "business_highest_ticket_sales_amt": 0,
            "ownership_entity_type": "L",
            "mcc_code": "1111",
            "full_mcc_code": "7841C"
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
                "signer_signed": "0",
                "owner_ref": "60c671b4ca31893ef7700000",
                "contacts": [
                    {
                        "contact_ref": "60c671b4ca31893ef7700000",
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
        "_id": "60c671b4ca31893ef700000",
        "parent_pfac_node_external_id": "PEIDB-00000-00000-00000-00000-00000-00000",
        "multiple_outlet": "0",
        "application_reference": "333000000000",
        "bank_lock": "0",
        "application_resubmitted": "0",
        "hierarchy_linking_flag": "0",
        "correspondence_language": "en_gb",
        "application_status_external_id": "APSE6-00000-00000-00000-00000-00000-00000",
        "documents": [],
        "funding_settings": {
            "application_reference": "333000000000",
            "settlement_method": "2",
            "chargeback_settlement_method": "1",
            "take_reserves_flag": "1",
            "funding_level": "1",
            "billing_level": "1",
            "reserve_entity_level": "2",
            "funding": {
                "use_default_config_for_all_nodes": "1",
                "configs": [
                    {
                        "entity_key": "DEFAULT",
                        "funding_frequency": "1",
                        "delay_funding_flag": "1",
                        "funding_delay_days": "2"
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
                        "reserve_type": "1"
                    }
                ]
            }
        }
    },
    "outlets": [
        {
            "merchant_hierarchy_template_external_id": "MHT45-00000-00000-00000-00000-00000-00000",
            "outlet_external_id": "OTL11-00000-00000-00000-00000-00000-00000",
            "pfac_node_external_id": "PEID2-00000-00000-00000-00000-00000-00000",
            "merchant_node_external_id": "MEI7D-00000-00000-00000-00000-00000-00000",
            "merchant_node_id": "13363",
            "root_merchant_node_id": "13357",
            "pfac_node_id": "1",
            "currencies": "USD",
            "accounts_setup_flag": "0",
            "billing_flag": "0",
            "billing_frequency": "1",
            "funding_flag": "0",
            "funding_frequency": "1",
            "delay_funding_flag": "0",
            "funding_delay_days": "1",
            "reserve_flag": "0",
            "reserve_type": "1",
            "set_reserve_target": "0",
            "hold_suspend_flag": "0",
            "date_added": "2021-06-13 21:21:03",
            "date_updated": "2021-06-13 21:21:03",
            "outlet_ref": "60c676bfd862d70883400000",
            "trade_name": "API outlet 31",
            "store_number": "12",
            "primary_email_address": "",
            "outlet_website": "",
            "internal_mid": "709900000001447",
            "mcc_code": "5411",
            "prod_serv_sold": "Convenience Store",
            "annual_card_turnover": "150000",
            "avg_ticket_sales_amt": "11111",
            "highest_ticket_sales_amt": "12",
            "sales_mail_perc": "0",
            "sales_phone_perc": "0",
            "sales_ftf_perc": "100",
            "sales_internet_perc": "0",
            "average_delivery_days": "5",
            "annual_turnover": "200000",
            "delivery_0_days_perc": "100",
            "delivery_1_to_7_days_perc": "0",
            "delivery_8_to_14_days_perc": "0",
            "delivery_15_to_30_days_perc": "0",
            "delivery_over_30_days_perc": "0",
            "sales_keyed_perc": "0",
            "contacts": {
                "60c676bfd862d7088346f9a2": {
                    "contact_type": "OT",
                    "contact_title": "Mr.",
                    "contact_first_name": "John",
                    "contact_second_name": "S",
                    "contact_last_name": "Snow",
                    "country_code": "840",
                    "city": "City",
                    "zip_code": "12345",
                    "county_code": "CA",
                    "email_address": "technologi@ technologi.co.uk",
                    "ent_telephone_code": "GB|44",
                    "telephone_number": "7425325869",
                    "floor": "1",
                    "street_number": "",
                    "suite_apart_number": "2"
                },
                "contact_metadata": []
            }
        }
    ],
    "merchant_sub_groups": [
        {
            "sub_group_external_id": "MSG62-00000-00000-00000-00000-00000-00000",
            "pfac_node_external_id": "PEID2-00000-00000-00000-00000-00000-00000",
            "merchant_node_external_id": "MEIAB-00000-00000-00000-00000-00000-00000",
            "merchant_node_id": "13360",
            "sub_group_data_id": "60c671b4ca31893ef7700000",
            "sub_group_type": "CHAIN",
            "parent_mid": "700100000002930",
            "internal_mid": "700100000002931",
            "same_as_outlet_mid": "1",
            "group_name": "SUB GROUP",
            "root_merchant_node_id": "13357",
            "billing_flag": "0",
            "funding_flag": "0",
            "reserve_flag": "0",
            "delay_funding_flag": "0",
            "hold_suspend_flag": "0",
            "merchant_hierarchy_template_external_id": "MHTE0-00000-00000-00000-00000-00000-00000",
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
                    "_id": "60c671b4ca31893ef77a44f9"
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
                    "_id": "60c671b4ca31893ef77a44fa"
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
    ],
    "merchant_hierarchy": [
        {
            "merchant_node_external_id": "MEI3F-00000-00000-00000-00000-00000-00000",
            "pfac_node_external_id": "PEID2-00000-00000-00000-00000-00000-00000",
            "ancestor_external_id": "MEI3F-00000-00000-00000-00000-00000-00000",
            "descendant_external_id": "MEI3F-00000-00000-00000-00000-00000-00000",
            "billing_flag": "1",
            "funding_flag": "1",
            "internal_mid": "700100000002930",
            "hold_suspend_flag": "0",
            "depth": "0",
            "entity_type": "MERCHANT"
        },
        {
            "merchant_node_external_id": "MEIAB-00000-00000-00000-00000-00000-00000",
            "pfac_node_external_id": "PEID2-00000-00000-00000-00000-00000-00000",
            "ancestor_external_id": "MEI3F-00000-00000-00000-00000-00000-00000",
            "descendant_external_id": "MEIAB-00000-00000-00000-00000-00000-00000",
            "billing_flag": "0",
            "funding_flag": "0",
            "internal_mid": "700100000002931",
            "hold_suspend_flag": "0",
            "depth": "1",
            "entity_type": "SUB_MERCHANT_GROUP",
            "sub_group_type": "CHAIN"
        },
        {
            "merchant_node_external_id": "MEI7D-00000-00000-00000-00000-00000-00000",
            "pfac_node_external_id": "PEID2-00000-00000-00000-00000-00000-00000",
            "ancestor_external_id": "MEI3F-00000-00000-00000-00000-00000-00000",
            "descendant_external_id": "MEI7D-00000-00000-00000-00000-00000-00000",
            "billing_flag": "0",
            "funding_flag": "0",
            "internal_mid": "709900000001447",
            "hold_suspend_flag": "0",
            "depth": "2",
            "entity_type": "OUTLET",
            "outlet_number": 1
        }
    ],
    "tree_descendants": {
        "MEI3F-00000-00000-00000-00000-00000-00000": {
            "ancestor": {
                "merchant_node_external_id": "MEI3F-00000-00000-00000-00000-00000-00000"
            },
            "descendants": [
                {
                    "merchant_node_external_id": "MEIAB-00000-00000-00000-00000-00000-00000"
                }
            ]
        },
        "MEIAB-00000-00000-00000-00000-00000-00000": {
            "ancestor": {
                "merchant_node_external_id": "MEIAB-00000-00000-00000-00000-00000-00000"
            },
            "descendants": [
                {
                    "merchant_node_external_id": "MEI7D-00000-00000-00000-00000-00000-00000"
                }
            ]
        }
    },
    "merchant_hierarchy_configuration_templates": {
        "MHT2D-00000-00000-00000-00000-00000-00000": {
            "merchant_hierarchy_template_external_id": "MHT2D-00000-00000-00000-00000-00000-00000",
            "merchant_hierarchy_config_external_id": "MHC47-00000-00000-00000-00000-00000-00000",
            "page_config_external_id": "PCIB5-00000-00000-00000-00000-00000-00000",
            "entity_type": "MERCHANT",
            "hierarchy_depth": "1",
            "status": "1"
        },
        "MHTE0-00000-00000-00000-00000-00000-00000": {
            "merchant_hierarchy_template_external_id": "MHTE0-00000-00000-00000-00000-00000-00000",
            "merchant_hierarchy_config_external_id": "MHC47-00000-00000-00000-00000-00000-00000",
            "page_config_external_id": "PCIEC-00000-00000-00000-00000-00000-00000",
            "entity_type": "SUBGROUP",
            "hierarchy_depth": "2",
            "status": "1"
        },
        "MHT45-00000-00000-00000-00000-00000-00000": {
            "merchant_hierarchy_template_external_id": "MHT45-00000-00000-00000-00000-00000-00000",
            "merchant_hierarchy_config_external_id": "MHC47-00000-00000-00000-00000-00000-00000",
            "page_config_external_id": "PCI7F-00000-00000-00000-00000-00000-00000",
            "entity_type": "OUTLET",
            "hierarchy_depth": "3",
            "status": "1"
        }
    },
    "substatuses": [],
    "application_default": [
        {
            "app_default_field_id": "29",
            "readonly": "0",
            "field_name": "merchant_hierarchy_config_id",
            "entity_block": "BUSINESS",
            "default_value": "15"
        },
        {
            "app_default_field_id": "51",
            "readonly": "1",
            "field_name": "parent_pfac_node_id",
            "entity_block": "BUSINESS",
            "default_value": "4"
        },
        {
            "app_default_field_id": "72",
            "readonly": "0",
            "field_name": "billing_frequency",
            "entity_block": "BUSINESS",
            "default_value": "1"
        },
        {
            "app_default_field_id": "57",
            "readonly": "1",
            "field_name": "chargeback_settlement_method",
            "entity_block": "BUSINESS",
            "default_value": "1"
        },
        {
            "app_default_field_id": "54",
            "readonly": "0",
            "field_name": "settlement_method",
            "entity_block": "BUSINESS",
            "default_value": "2"
        },
        {
            "app_default_field_id": "60",
            "readonly": "0",
            "field_name": "take_reserves_flag",
            "entity_block": "BUSINESS",
            "default_value": "1"
        },
        {
            "app_default_field_id": "63",
            "readonly": "1",
            "field_name": "reserve_entity_level",
            "entity_block": "BUSINESS",
            "default_value": "2"
        },
        {
            "app_default_field_id": "75",
            "readonly": "0",
            "field_name": "funding_frequency",
            "entity_block": "BUSINESS",
            "default_value": "1"
        },
        {
            "app_default_field_id": "78",
            "readonly": "0",
            "field_name": "delay_funding_flag",
            "entity_block": "BUSINESS",
            "default_value": "1"
        },
        {
            "app_default_field_id": "87",
            "readonly": "0",
            "field_name": "reserve_type",
            "entity_block": "BUSINESS",
            "default_value": "1"
        },
        {
            "app_default_field_id": "66",
            "readonly": "0",
            "field_name": "funding_level",
            "entity_block": "BUSINESS",
            "default_value": "1"
        },
        {
            "app_default_field_id": "69",
            "readonly": "0",
            "field_name": "billing_level",
            "entity_block": "BUSINESS",
            "default_value": "1"
        },
        {
            "app_default_field_id": "81",
            "readonly": "0",
            "field_name": "funding_delay_days",
            "entity_block": "BUSINESS",
            "default_value": "2"
        },
        {
            "app_default_field_id": "22",
            "readonly": "1",
            "field_name": "mcc_code",
            "entity_block": "BUSINESS",
            "default_value": "7841C"
        },
        {
            "tenant_default_field_id": "145",
            "app_default_field_id": "1",
            "default_value": "NEW",
            "language_code": "en_gb",
            "status": "1",
            "readonly": "1",
            "field_name": "ent_amex_merchant_type",
            "answer_type": "OPTION",
            "param_code": null,
            "entity_block": "ALL_OUTLET",
            "page_config_path": "TradingInformation.block_amex.ent_amex_merchant_type",
            "no_default": "0",
            "description": "AMEX Merchant Type?"
        },
        {
            "tenant_default_field_id": "192",
            "app_default_field_id": "102",
            "default_value": "1",
            "language_code": "en_gb",
            "status": "2",
            "readonly": "0",
            "field_name": "billing_flag",
            "answer_type": "OPTION",
            "param_code": null,
            "entity_block": "ALL_OUTLET",
            "page_config_path": null,
            "no_default": "0",
            "description": "Billing Flag"
        },
        {
            "tenant_default_field_id": "258",
            "app_default_field_id": "13",
            "default_value": "7841C",
            "language_code": "en_gb",
            "status": "1",
            "readonly": "0",
            "field_name": "mcc_code",
            "answer_type": "LIST",
            "param_code": "MCC_CODES_PARAM",
            "entity_block": "ALL_OUTLET",
            "page_config_path": "TradingInformation.block_general_information.mcc_iso",
            "no_default": "0",
            "description": "MCC"
        },
        {
            "tenant_default_field_id": "264",
            "app_default_field_id": "30",
            "default_value": "1",
            "language_code": "en_gb",
            "status": "1",
            "readonly": "1",
            "field_name": "visitation_required",
            "answer_type": "OPTION",
            "param_code": null,
            "entity_block": "ALL_OUTLET",
            "page_config_path": "BusinessInformation.block_application_options.site_survey",
            "no_default": "0",
            "description": "Site Survey?"
        }
    ],
    "has_generated_documents": "1"
}



```
