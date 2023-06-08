# Sub-merchant Onboarding

## Boarding by API

Exchange offers end-to-end sub-merchant onboarding through API that is facilitated through Adding Applications, Subgroups and Outlets in order to create the correct sub-merchant hierarchy. This includes adding, and updating sub-merchant applications in progress before submitting them.

For the standard merchant - chain - outlet Hierarchy, three calls are needed to submit an application.
This can include pricing and equipment for the sub-merchant  that is required, and the billing and funding settings for the sub-merchant. 

<!-- !align: center -->
![hierarchy](/assets/images/hierarchy.png)

### Adding the sub-merchant and chain levels

<!--
type: tab
titles: Add Application, JSON Add Application Example
-->

The `/boarding/application` endpoint supports adding the merchant and chain level in one request. This will require legal information to be sent, principal information , application settings and an offer package if used for adding processing offerings or equipement offerings.

---

<!-- type: tab -->

JSON format for `ADD_APPLICATION`:

```json
    "operation": {
        "operation_type": "ADD_APPLICATION",
        "version": "2.0.0"
    },
    "merchant": {
        "billing_level": "3",
        "funding_level": "3",
        "funding_settings": {
            "delay_funding_flag": "0",
            "reserve_type": "1",
            "set_reserve_target": "0",
            "billing_frequency": "1",
            "funding_frequency": "1"
        },
        "pricing_level": "BUSINESS",
        "take_reserves_flag": "1",
        "reserve_entity_level": "1",
        "settlement_method": "1",
        "allow_split_flag": "0",
        "business_entity": {
            "legal_name": "MMISTest Example",
            "ownership_entity_type": "L",
            "tin_type": "2",
            "business_tin_ssn_number": "410520145",
            "irs_filing_name": "MMISTest Example",
            "business_category": "R",
            "application_type": "RETAIL",
            "project_name": "test",
            "security_code": "4000",
            "reg_number": "023457014",
            "mcc_code": "5999",
            "date_incorporated": "2010-01-20",
            "foundation_date": "2010-01-20",
            "incorp_state": "CA",
            "foreign_entity": "0",
            "irs_status": "N"
        },
        "registration_address": {
            "zip_code": "12345",
            "suite_apart_number": "1",
            "floor": "1",
            "street_line_1": "High Street",
            "street_line_2": "Northam Way",
            "city": "City",
            "county_code": "CA",
            "country_code": "840"
        },
        "owners": [
            {
                "owner_title": "Ms.",
                "owner_first_name": "Jane",
                "owner_second_name": "",
                "owner_surname": "Doe",
                "contact_dob": "1994-07-13",
                "owner_nationality": "826",
                "owner_position": "OW",
                "owner_phone_code": "US|1",
                "owner_phone_no": "7234567893",
                "owner_date_started": "2019-12-12",
                "owner_email": "technologi@technologi.co.uk",
                "owner_tin_ssn_number": "111989898",
                "is_main_principal": "1",
                "ownership_perc": "100",
                "personal_guarantee": "Y",
                "contacts": [
                    {
                        "zip_code": "12345",
                        "suite_apart_number": "1",
                        "floor": "5",
                        "province": "t",
                        "street_line_1": "Street Example 1",
                        "street_line_2": "Street Exanmple",
                        "city": "City Example",
                        "county_code": "CA",
                        "date_from": "2020-05-29",
                        "country_code": "840"
                    }
                ]
            }
        ],
        "merchant_sub_group": {
            "group_name": "SUB GROUP"
        }
    }
}
```

<!-- type: tab-end -->

---

### Adding the Outlet

<!--
type: tab
titles: Add Outlet, JSON Add Outlet Example
-->

The `/boarding/outlet` endpoint supports adding the outlet to an application, and will require the application reference and the parent MID of where the outlet should be added to be added to the request. This will be retrieved from the `ADD_APPLICATION` request, and the parent MID will be the `internal_mid` of the merchant applications subgroup (as to add for the standard merchant-chain-outlet hierarchy).



---

<!-- type: tab -->

JSON format for `ADD_OUTLET`:

```json
{
    "request_source": {
        "initiator": "ALLIANCE",
        "alliance_code": "DEMO"
    },
    "operation": {
        "operation_type": "ADD_OUTLET",
        "version": "2.0.0"
    },
    "application": {
        "application_reference": "XXXXXXX"
    },
    "outlet": {
        "parent_mid": "XXXXXXX",
        "trade_name": "outlet",
        "outlet_website": "http://netpay.co.uk",
        "pricing_type": "002",
        "store_number": "12",
        "primary_email_address": "technologi@technologi.co.uk",
        "business_zone": "B",
        "business_location": "H",
        "ground_floor": "O",
        "square_foot_count": "1",
        "number_of_building_floors": "2",
        "visitation_required": "0",
        "statement_type": "F",
        "number_of_employees": "12",
        "statement_delivery_method": "P",
        "mcc_code": "5999",
        "seasonal_business": "1",
        "seasonal_start_month": "JANUARY",
        "seasonal_end_month": "FEBRUARY",
        "currencies": "USD",
        "mastercard_sales": "300000",
        "visa_sales": "300000",
        "visa_mastercard_sales": "600000",
        "turnover_bus_to_bus_perc": "0",
        "turnover_bus_to_cons_perc": "100",
        "card_bus_to_bus_perc": "0",
        "card_bus_to_cons_perc": "100",
        "highest_ticket_sales_amt": "100",
        "sales_ftf_perc": "100",
        "sales_keyed_perc": "0",
        "sales_phone_perc": "0",
        "sales_mail_perc": "0",
        "sales_internet_perc": "0",
        "sales_tradeshow_perc": "0",
        "annual_turnover": "600000",
        "annual_card_turnover": "600000",
        "average_delivery_days": "0",
        "delivery_0_days_perc": "100",
        "delivery_1_to_7_days_perc": "0",
        "delivery_8_to_14_days_perc": "0",
        "delivery_15_to_30_days_perc": "0",
        "delivery_over_30_days_perc": "0",
        "prod_serv_sold": "SELLING",
        "sales_moto_perc": "0",
        "avg_ticket_sales_amt": "10",
        "chip_flag": "Y",
        "recurring_flag": "1",
        "transaction_process_mode": "2",
        "has_full_pmnt_bef_del": "0",
        "contacts": [
            {
                "contact_type": "OT",
                "contact_title": "Mr.",
                "contact_first_name": "Jane",
                "contact_last_name": "Doe",
                "country_code": "840",
                "city": "City",
                "zip_code": "12345",
                "street_line_1": "Example Street",
                "county_code": "CA",
                "floor": "1",
                "suite_apart_number": "2",
                "house_number": "13",
                "house_name": "",
                "email_address": "technologi@technologi.co.uk",
                "ent_telephone_code": "US|01",
                "telephone_number": "742345678"
            },
            {
                "contact_type": "B",
                "contact_title": "Ms.",
                "contact_first_name": "Jane",
                "contact_last_name": "Doe",
                "country_code": "840",
                "city": "City",
                "zip_code": "12345",
                "street_line_1": "Example Street 1",
                "county_code": "CA",
                "floor": "1",
                "suite_apart_number": "2",
                "house_number": "13",
                "house_name": "Dolos",
                "email_address": "technologi@technologi.co.uk,
                "ent_telephone_code": "US|01",
                "telephone_number": "723566455",
            }
        ],
        "online_offer": {
            "equipment_offering_external_id": "EQO71-XXXXX",
            "selected_offer_item": null,
            "bundles": [
                {
                    "equipment_bundle_external_id": "EQOB1-XXXXX",
                    "equipment_bundle_item_external_id": "EBIE6-XXXXX",
                    "bundle_name": "SYSTEM_GENERATED",
                    "is_boarding_activated": null,
                    "bundle_items": [
                        {
                            "equipment_bundle_item_external_id": "EBIE6-XXXXX",
                            "is_mandatory": "0",
                            "is_invisible": "0",
                            "service": {
                                "service_external_id": "PRO2F-XXXXX",
                                "service_type": "VAR",
                                "service_name": " Gateway",
                                "service_api_code": "99201",
                                "service_for": "ECOM",
                                "service_for_group": "ONLINE_PRODUCT"
                            },
                            "service_charges": [
                                {
                                    "service_charge_item_external_id": "SCIAD-XXXXX",
                                    "alliance_external_id": "ALLE4-XXXXX",
                                    "service_item_name": "Owned",
                                    "service_item_type": "2",
                                    "service_item_for": "1",
                                    "service_frequency": "1",
                                    "order_by": "27",
                                    "service_ownership": "1",
                                    "charge_decimals": "2",
                                    "is_selected": "1",
                                    "item_status": "1",
                                    "instalment_available": "2",
                                    "language_code": "en_gb",
                                    "date_added": "2022-06-11 16:20:17",
                                    "fee_type": "3",
                                    "minimum_base_charge": "0.00",
                                    "maximum_base_charge": "0.00",
                                    "default_base_charge": "0.00",
                                    "base_charge": "0.00",
                                    "minimum_perc_charge": "0.00",
                                    "maximum_perc_charge": "0.00",
                                    "default_perc_charge": "0.00",
                                    "perc_charge": "0.00"
                                }
                            ]
                        }
                    ]
                }
            ],
            "agreement_length": null
        },
        "banks": [
            {
                "bank_name": "Bank of America",
                "bank_city": "ATMORE",
                "country_code": "840",
                "zip_code": "36502-8856",
                "county_code": "AL",
                "street_line_1": "JACK SPRINGS RD",
                "floor": "",
                "suite_apart_number": "",
                "province": "ESCAMBIA ALABAMA",
                "account_holder_name": "Test Account",
                "account_type": [
                    "CREDIT",
                    "DEBIT",
                    "CHARGEBACK"
                ],
                "bank_account_type": "CHECKING",
                "dda_number": "4642355454",
                "routing_number": "123456789"
            }
        ]
    }
}
```

<!-- type: tab-end -->

---

### Submitting an Application

<!--
type: tab
titles: Application Submit, JSON Application Submit Example
-->

The `/boarding/application` endpoint supports submitting the application for the reference parsed. This requires the operation type `APPLICATION_SUBMIT` to be added to the request. Please see adjacent example for this. Any validation errors will return a `success` : 0 , with the errors detailed in the bottom of the response with where they need to be updated. This would require the application to be updated, and resubmit until it passes the validation. For full specs on this please see the  [API explorer](../api?type=post&path=/v1/apis).

---

<!-- type: tab -->

JSON format for `APPLICATION_SUBMIT`:

```json
{
    "request_source": {
        "initiator": "ALLIANCE",
        "alliance_code": "ALLIANCE"
    },
    "operation": {
        "operation_type": "APPLICATION_SUBMIT",
        "version": "2.0.0"
    },
    "application": {
        "application_reference": "33300XXXXXXXX"
    }
}
```

<!-- type: tab-end -->

---

### Updating an Application

While an Application is in 'Open' status, this can be updated using the UPDATE requests, of which can be done for each level of the sub-merchant.
An applications status and information can be retrieved using the `APPLICATION_STATUS_CHECK` and `RETRIEVE_APPLICATION` requests, and a complete application can be submit by using the `APPLICATION_SUBMIT` request (pending validation). 
Applications that are invalid will respond with the errors and their locations so that the entity may be updated, and resubmit. 

<!--
type: tab
titles: Update Merchant, JSON Update Merchant Example 
-->

The `/boarding/merchant` endpoint supports updating for the merchant level and subgroup level, while the `/boarding/outlet` allows the outlet to be updated.
To update the outets and subgroups , the `outlet_external_id` or `sub_group_external_id` must also be added to the request to specify the outlet/sub group, which can be found using the `RETRIEVE_MERCHANT_HIERARCHY` operation at the `/boarding/application` endpoint (see [API specs for this request](../api?type=post&path=/v1/apis)).
The application reference must be added to the request, and operation type based on the update being made.

- UPDATE_MERCHANT at `/boarding/merchant` for merchant level.
- UPDATE_MERCHANT_SUB_GROUP at `/boarding/merchant` for subgroup level.
- UPDATE_OUTLET at `/boarding/outlet` for outlet level.

---

<!-- type: tab -->

JSON format for `UPDATE_MERCHANT`:

```json
{
    "request_source": {
        "initiator": "ALLIANCE",
        "alliance_code": "ALLIANCE"
    },
    "operation": {
        "operation_type": "UPDATE_MERCHANT",
        "version": "2.0.0"
    },
    "application": {
        "application_reference": "3330XXXXX"
    },
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

---
