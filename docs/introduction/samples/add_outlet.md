# ADD_OUTLET

## `/boarding/outlet`

### REQUEST:
```
{
   "request_source":{
      "initiator":"ALLIANCE",
      "alliance_code":"technologi"
   },
   "operation":{
      "operation_type":"ADD_OUTLET",
      "version":"2.0.0"
   },
   "application":{
      "application_reference":"33300000000"
   },
   "outlet":{
      "parent_mid":"700100000002931",
      "trade_name":"API outlet 31",
      "outlet_website":"",
      "store_number":"12",
      "mcc_code":"5411",
      "currencies":"USD",
      "primary_email_address":"",
      "highest_ticket_sales_amt":"12",
      "sales_ftf_perc":"100",
      "sales_keyed_perc":"0",
      "sales_phone_perc":"0",
      "sales_mail_perc":"0",
      "sales_internet_perc":"0",
      "annual_turnover":"200000",
      "annual_card_turnover":"150000",
      "average_delivery_days":"5",
      "delivery_0_days_perc":"100",
      "delivery_1_to_7_days_perc":"0",
      "delivery_8_to_14_days_perc":"0",
      "delivery_15_to_30_days_perc":"0",
      "delivery_over_30_days_perc":"0",
      "prod_serv_sold":"Convenience Store",
      "avg_ticket_sales_amt":"11111",
      "contacts":[
         {
            "contact_type":"OT",
            "contact_title":"Mr.",
            "contact_first_name":"John",
            "contact_second_name":"S",
            "contact_last_name":"Snow",
            "floor":"1",
            "suite_apart_number":"2",
            "street_number":"",
            "city":"City",
            "county_code":"CA",
            "country_code":"840",
            "zip_code":"12345",
            "ent_telephone_code":"GB|44",
            "telephone_number":"07425325869",
            "email_address":"technologi@technologi.co.uk"
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
        "operation_type": "ADD_OUTLET",
        "version": "2.0.0"
    },
    "merchant": {
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
        "date_updated": "2021-06-13 20:59:32",
        "pfac_node_external_id": "PEID2-00000-00000-00000-00000-00000-00000"
    },
    "outlet": {
        "merchant_hierarchy_template_external_id": "MHT45-00000-00000-00000-00000-00000-00000",
        "outlet_external_id": "OTL11-00000-00000-00000-00000-00000-00000",
        "pfac_node_external_id": "PEID2-00000-00000-00000-00000-00000-00000",
        "merchant_node_external_id": "MEI7D-00000-00000-00000-00000-00000-00000",
        "merchant_node_id": "13363",
        "root_merchant_node_id": "13357",
        "pfac_node_id": "1",
        "trade_name": "API outlet 31",
        "currencies": "USD",
        "billing_flag": 0,
        "billing_frequency": "1",
        "funding_flag": 0,
        "funding_frequency": "1",
        "delay_funding_flag": "0",
        "funding_delay_days": "1",
        "reserve_flag": 0,
        "reserve_type": "1",
        "set_reserve_target": "0",
        "date_added": "2021-06-13 21:21:03",
        "date_updated": "2021-06-13 21:21:03",
        "outlet_ref": "60c676bfd862d70883400000",
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
}



```
