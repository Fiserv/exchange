#  ADD_MERCHANT_SUBGROUP

## `/boarding/merchant`

### REQUEST:
```
{
    "request_source": {
        "initiator": "ALLIANCE",
        "alliance_code": "MOTIONSOFT"
    },
    "operation": {
        "operation_type": "ADD_MERCHANT_SUB_GROUP",
        "version": "2.0.0"
    },
    "application": {
        "application_reference": "333000003186"
    },
    "merchant_sub_group": {
        "parent_mid":"700100000002930",
        "group_name": "My Chain",
        "contacts": [
      {
        "contact_type": "L",
        "contact_title": "Mr.",
        "contact_first_name": "John",
        "contact_last_name": "Snow",
        "country_code": "840",
        "contact_second_name": "S",
        "city": "City",
        "zip_code": "12345",
        "street_line_1": "BerlinStreet",
        "county_code": "NY",
        "floor":"1",
        "street_number":"",
        "locality":"",
        "suite_apart_number":"2",
        "email_address": "technologi@technologi.co.uk",
        "ent_telephone_code": "US|1",
        "telephone_number": "07425325869"
      }
    ]
    }
}
```

### RESPONSE:
```
{
    "result": "SUCCESS",
    "operation": {
        "operation_type": "ADD_MERCHANT_SUB_GROUP",
        "version": "2.0.0"
    },
    "merchant": {
        "merchant_node_external_id": "MEI3F-00000-00000-00000-00000-00000-00000",
        "sales_owner_user_external_id": "USR19-00000-00000-00000-00000-00000-00000",
        "risk_owner_user_external_id": "USR19-00000-00000-00000-00000-00000-00000",
        "creator_user_external_id": "USR19-00000-00000-00000-00000-00000-00000",
        "alliance_external_id": "ALL95-00000-00000-00000-00000-00000-00000",
        "internal_mid": "700100000002930",
        "billing_frequency": "1",
        "hold_suspend_flag": "0",
        "funding_frequency": "1",
        "settlement_method": "2",
        "parent_type": "ALLIANCE",
        "reserve_entity_level": "2",
        "reserve_flag": "1",
        "language_code": "en_gb",
        "date_added": "2021-06-13 20:59:32",
        "date_updated": "2021-06-13 22:27:03",
        "pfac_node_external_id": "PEID2-00000-00000-00000-00000-00000-00000",
        "registered_address": {
            "city": "City",
            "street_line_1": "High Street",
            "zip_code": "12345",
            "country_code": "840"
        },
        "owner": {
            "contact_title": "Mr.",
            "contact_first_name": "Bailey",
            "contact_last_name": "Woods",
            "contact_address1": "High Street",
            "contact_town_city": "City",
            "contact_postcode": "12345",
            "contact_country_code": "840",
            "contact_position": "OW"
        }
    },
    "merchant_sub_group": {
        "sub_group_external_id": "MSGC6-00000-00000-00000-00000-00000-00000",
        "pfac_node_external_id": "PEID2-00000-00000-00000-00000-00000-00000",
        "merchant_node_external_id": "MEI83-00000-00000-00000-00000-00000-00000",
        "merchant_node_id": "13366",
        "sub_group_data_id": "60c68ca6ca31893ef7700000",
        "sub_group_type": "CHAIN",
        "parent_mid": "700100000002930",
        "internal_mid": "700100000002932",
        "group_name": "My Chain",
        "root_merchant_node_id": "13357",
        "billing_flag": 0,
        "funding_flag": 0,
        "funding_frequency": "0",
        "reserve_flag": 0,
        "reserve_type": "1",
        "set_reserve_target": "0",
        "delay_funding_flag": "0",
        "merchant_hierarchy_template_external_id": "MHTE0-00000-00000-00000-00000-00000-00000",
        "accounts_setup_flag": null,
        "contacts": [
            {
                "contact_type": "L",
                "contact_title": "Mr.",
                "contact_first_name": "John",
                "contact_second_name": "S",
                "contact_last_name": "Snow",
                "country_code": "840",
                "city": "City",
                "zip_code": "12345",
                "street_line_1": "BerlinStreet",
                "county_code": "NY",
                "email_address": "technologi@technologi.co.uk",
                "ent_telephone_code": "US|1",
                "telephone_number": "07425325869",
                "floor": "1",
                "street_number": "",
                "suite_apart_number": "2"
            }
        ]
    }
}
```
