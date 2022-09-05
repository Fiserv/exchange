# Offerings

## Pricing and Equipment
Exchange supports pricing and equipment added to Applications through the use of offerings and offer packages. Offerings are split into three types: Processsing, Equipment and Online. These offerings are created by the PayFac and added to an Offer Package, which can then be retrieved from the `/offering/avaliable` endpoint. Upon retrieving an Offer Package, the offerings avaliable in the package will be listed. Online and Equipment offerings can be retrieved by using the `/offering/equipment` endpoint for their full details. A selected Offering (by external ID) can have detals grabbed in order to retrieve the pricing information and equipment information.

Processing offerings (that contain transaction pricing and acquiring charges) may be retrieved by using the `/offering/processing` endpoint and providing the desired external ID. 
Processing offerings will be added to the sub-merchants **pricing level**, and equipment/online offerings at the outlet.

## Adding a standard offer package and offerings

In order to add a standard offer package and to apply the offerings configured during boarding, we must follow a few steps on retrieving the information required to add.

### Retrieving the offer package

First, we must retrieve the offer package that contains the equipment offerings and processing offerings we want to add. For this, we call the `/offering/avaliable` endpoint. This will specify all currently configured offering packages and return the `external_id` of any offering contained in the offer package. We can then use the `external_id` to gather more information about the offering to add to applications during boarding. 

<!--
type: tab
titles: Available Offer Packages Request, Available Offer Packages Response
-->

JSON format request for `LIST_AVAILABLE_OFFERINGS`:

```json
{
    "request_source": {
        "initiator": "ALLIANCE",
        "alliance_code": "ALLIANCE"
    },
    "operation": {
        "operation_type": "LIST_AVAILABLE_OFFERINGS",
        "version": "2.0.0"
    }
}
```
---

<!-- type: tab -->

JSON format response for `LIST_AVAILABLE_OFFERINGS`:

```json
{
	"Example package name": {
		"package_external_id": "TPXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
		"package_name": "Example package name",
		"offer_code": "6565",
		"package_weight": "100",
		"package_channel": "3",
		"package_status": "1",
		"non_processing_flag": "0",
		"offer_code_status": "1",
		"processing_offers": [
			{
				"transaction_pricing_external_id": "TPXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
				"alliance_external_id": "DEXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
				"acquirer_external_id": "MACXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
				"processing_platform": "OTHER",
				"transaction_pricing_name": "ProcessingPricing",
				"transaction_pricing_ref": "12345",
				"non_processing_flag": "0",
				"fee_collection_type": "INTERCHANGE",
				"currency": "USD",
				"is_tier_price": "0",
				"tier_price_type": "1",
				"tiers": [
					{
						"from": "1"
					}
				],
				"language_code": "en_gb"
			}
		],
		"equipment_offers": [
			{
				"offering_name": "EquipmentOffering",
				"equipment_terminal_network": "NASHVILLE",
				"acquiring_only": "0",
				"equipment_offering_ref": "",
				"language_code": "en_gb",
				"is_dcc": "0",
				"equipment_offering_external_id": "EQXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX"
			}
		],
		"online_offers": [
			{
				"offering_name": "OnlineOffering",
				"equipment_terminal_network": "NASHVILLE",
				"acquiring_only": "0",
				"equipment_offering_ref": "",
				"language_code": "en_gb",
				"is_dcc": "0",
				"equipment_offering_external_id": "EQXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX"
			}
		]
	}
}
```
Used to return package and offering `external_id` that may be used for boarding if configured criteria is applicable to the application.
<!-- type: tab-end -->

---
### Retrieving the processing offering

Using the information from the offer package response, we can now use the `/offering/processing` endpoint to retrieve information about the specified processing offering using its `external_id`. For the example below, we want to gather the information configured for the processing offering above with `"transaction_pricing_external_id"` *"TPI6B-34KLA-F81C9-B9617-08C45-6A1B1-2B8E6"*

<!--
type: tab
titles: Specified Processing Offering Request, Specified Processing Offering Response
-->

JSON format request for `RETRIEVE_PROCESSING_OFFERING`:

```json
{
    "request_source": {
        "initiator": "ALLIANCE",
        "alliance_code": "ALLIANCE"
    },
    "operation": {
        "operation_type": "RETRIEVE_PROCESSING_OFFERING",
        "version": "2.0.0"
    },
    "processing_offering":{
        "transaction_pricing_external_id":"TPXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX"
    }

}
```
---

<!-- type: tab -->

JSON format response for `RETRIEVE_PROCESSING_OFFERING`:

```json
{
    "result": "SUCCESS",
    "operation": {
        "operation_type": "RETRIEVE_PROCESSING_OFFERING",
        "version": "2.0.0"
    },
    "charge_item_groups": [
        {
            "charge_item_group_external_id": "CIXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
            "alliance_external_id": "ALXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
            "acquirer_external_id": "MAXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
            "processing_platform": "OTHER",
            "fee_collection_type": "INTERCHANGE",
            "charge_item_group_name": "Transaction Group",
            "charge_item_group_ref": "147852",
            "order_by": "2",
            "item_status": "1",
            "language_code": "en_gb",
            "date_added": "2021-06-17 17:33:50",
            "charge_items": [
                {
                    "charge_item_external_id": "CHXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                    "alliance_external_id": "ALXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                    "acquirer_external_id": "MAXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                    "processing_platform": "OTHER",
                    "charge_item_name": "Transaction Charge",
                    "charge_item_ref": "14785",
                    "fee_collection_type": "INTERCHANGE",
                    "is_merged_charges": "0",
                    "charge_decimals": "2",
                    "order_by": "3",
                    "item_status": "1",
                    "language_code": "en_gb",
                    "date_added": "2021-06-17 17:29:27",
                    "charges": [
                        {
                            "charge_item_external_id": "CHXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                            "category": "1",
                            "fee_type": "2",
                            "minimum_base_charge": "10.00000",
                            "maximum_base_charge": "10.00000",
                            "default_base_charge": "10.00000",
                            "status": "1"
                        }
                    ],
                    "transaction_pricing_external_id": "TPXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                    "charge_item_group_external_id": "CIXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                    "is_activated": "1",
                    "is_mandatory": "0",
                    "is_invisible": "0",
                    "charge_item_prices": [
                        {
                            "charge_item_price_charges": [
                                {
                                    "tier_number": "0",
                                    "fee_type": "2",
                                    "category": "1",
                                    "minimum_base_charge": "10.00",
                                    "maximum_base_charge": "10.00",
                                    "default_base_charge": "10.00",
                                    "transaction_pricing_external_id": "TPXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                                    "charge_item_group_external_id": "CIXXX-XXXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                                    "charge_item_external_id": "CHXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX"
                                }
                            ]
                        }
                    ]
                }
            ]
        }
    ],
    "service_charge_items": [
        {
            "service_charge_item_external_id": "SCXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
            "alliance_external_id": "ALXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
            "acquirer_external_id": "MAXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
            "service_item_name": "Service Item",
            "service_item_type": "1",
            "service_frequency": "1",
            "processing_platform": "OTHER",
            "order_by": "108",
            "service_ownership": "1",
            "charge_decimals": "2",
            "charge_ref": "147852",
            "item_status": "1",
            "instalment_available": "1",
            "language_code": "en_gb",
            "date_added": "2021-06-17 17:39:06",
            "transaction_pricing_external_id": "TPXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
            "is_activated": "1",
            "is_mandatory": "0",
            "is_invisible": "0",
            "service_item_charges": [
                {
                    "fee_type": "2",
                    "minimum_base_charge": "10.00",
                    "maximum_base_charge": "10.00",
                    "default_base_charge": "10.00",
                    "transaction_pricing_external_id": "TPXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                    "service_charge_item_external_id": "SCXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX"
                }
            ],
            "charges": [
                {
                    "service_charge_item_external_id": "SCXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                    "fee_type": "2",
                    "minimum_base_charge": "10.00",
                    "maximum_base_charge": "10.00",
                    "default_base_charge": "10.00",
                    "status": "1"
                }
            ]
        }
    ]
}
```
<!-- type: tab-end -->

---

We are able to view each of the charge items that have been configured to be available in the processing offering.

### Retrieving online and equipment offerings

To retrieve online and equipment offerings, we will repeat the process above using the `/offering/equipment` endpoint, where we specify the `external_id` for each in the `equipment_offering_external_id`.
```json
{
    "equipment_offering":{
        "equipment_offering_external_id":"XXXXX"
    }
}
```

## Adding the offerings during boarding

Now we have retrieved all the information required, we can start adding these during boarding. The `offer_package_external_id` for the offer package and the  processing offering will need to be added to the pricing level of the application, and the equipment will be added at the outlet. For the standard application, where pricing is added at the Business level, we add the processing offering and package in the `ADD_APPLICATION` request.

### Adding Offer Package and Processing offering to Application

In order to add this to the application, we must add the `"acquiring_offer"` and `"package_external_id"`. This is added within the `"merchant"` block.
The acquiring offer will be structured as seen below, where we will define the transaction pricing used (Processing offering), and the charge items from the processing offering we want to use. we will then define the actual charge we want to use for the offer, `perc_charge` and `base_charge`  in the `charge_item_price_charges`. The min, max and default are retrieved from the retrieval calls above. We also have to define identifiers for the object, using the information from the retrieval calls for the pricing. The items `"is_activated": "1",`, `"is_boarding_activated": "1",` should be used to indicate the charge is selected.

Please see below sample of an acquiring offer, and a sample of how this can be used in the add_application payload


<!--
type: tab
titles: Acquiring offer Block + Offer Package, Sample being used in ADD_APPLICATION
-->

JSON format for acquiring offer and offer package:

```json
"acquiring_offer": {
    "transaction_pricing_external_id": "TPXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
    "transaction_pricing_name": "Standard Entitlement",
    "transaction_pricing_ref": null,
    "currency": "USD",
    "is_tier_price": "0",
    "tier_price_type": "1",
    "fee_collection_type": "INTERCHANGE",
    "alliance_external_id": "ALXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
    "acquirer_external_id": "MAXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
    "processing_platform": "OTHER",
    "charge_items": [
        {
            "charge_item_external_id": "CHXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
            "charge_item_group_external_id": "CIXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
            "charge_item_name": "Visa Mastercard Discover",
            "charge_item_ref": "10011",
            "fee_collection_type": "INTERCHANGE",
            "charge_decimals": "2",
            "is_invisible": "0",
            "is_activated": "1",
            "is_boarding_activated": "1",
            "is_mandatory": "1",
            "is_merged_charges": "0",
            "charge_item_prices": [
                {
                    "charge_item_price_charges": [
                        {
                            "fee_type": "1",
                            "category": "3",
                            "minimum_perc_charge": "0.00000",
                            "maximum_perc_charge": "0.00000",
                            "default_perc_charge": "0.00000",
                            "perc_charge": "0.00000"
                        },
                        {
                            "fee_type": "2",
                            "category": "3",
                            "minimum_base_charge": "0.00000",
                            "maximum_base_charge": "0.00000",
                            "default_base_charge": "0.00000",
                            "base_charge": "0.00000"
                        }
                    ]
                }
            ]
        },
        {
            "charge_item_external_id": "CHTXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
            "charge_item_group_external_id": "CIGXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
            "charge_item_name": "AmexOptBlue",
            "charge_item_ref": "777-1000105251",
            "fee_collection_type": "INTERCHANGE",
            "charge_decimals": "2",
            "is_invisible": "0",
            "is_activated": "1",
            "is_boarding_activated": "1",
            "is_mandatory": "1",
            "is_merged_charges": "0",
            "charge_item_prices": [
                {
                    "charge_item_price_charges": [
                        {
                            "fee_type": "1",
                            "category": "3",
                            "minimum_perc_charge": "0.00000",
                            "maximum_perc_charge": "0.00000",
                            "default_perc_charge": "0.00000",
                            "perc_charge": "0.00000"
                        },
                        {
                            "fee_type": "2",
                            "category": "3",
                            "minimum_base_charge": "0.00000",
                            "maximum_base_charge": "0.00000",
                            "default_base_charge": "0.00000",
                            "base_charge": "0.00000"
                        }
                    ]
                }
            ]
        }
    ]
},
"package_external_id": "OPXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",

```
---

<!-- type: tab -->

JSON sample request in `ADD_APPLICATION`:

```json
{
    "request_source": {
        "initiator": "ALLIANCE",
        "alliance_code": "ALLIANCE"
    },
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
            "legal_name": "MMISTEST Legalname",
            "ownership_entity_type": "L",
            "tin_type": "1",
            "business_tin_ssn_number": "111989898",
            "irs_filing_name": "MMISTEST Legalname",
            "business_category": "R",
            "application_type": "RETAIL",
            "project_name": "test",
            "security_code": "4000",
            "reg_number": "1111111",
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
            "street_line_2": "Street Way",
            "city": "City",
            "county_code": "CA",
            "country_code": "840"
        },
        "owners": [
            {
                "owner_title": "Mr.",
                "owner_first_name": "First",
                "owner_second_name": "",
                "owner_surname": "Last",
                "contact_dob": "1994-07-13",
                "owner_nationality": "826",
                "owner_position": "OW",
                "owner_phone_code": "US|1",
                "owner_phone_no": "12345676667",
                "owner_date_started": "2019-12-12",
                "owner_email": "technologi@technologi.co.uk",
                "owner_tin_ssn_number": "111989898",
                "is_main_principal": "1",
                "ownership_perc": "100",
                "personal_guarantee": "Y",
                "contacts": [
                    {
                        "zip_code": "65890",
                        "suite_apart_number": "1",
                        "floor": "5",
                        "province": "t",
                        "street_line_1": "12 Street Way",
                        "street_line_2": "GOOD WAY",
                        "city": "SPRINGFIELD",
                        "county_code": "CA",
                        "date_from": "2020-05-29",
                        "country_code": "840"
                    }
                ]
            }
        ],
        "acquiring_offer": {
            "transaction_pricing_external_id": "TPXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
            "transaction_pricing_name": "Standard Entitlement",
            "transaction_pricing_ref": null,
            "currency": "USD",
            "is_tier_price": "0",
            "tier_price_type": "1",
            "fee_collection_type": "INTERCHANGE",
            "alliance_external_id": "ALXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
            "acquirer_external_id": "MAXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
            "processing_platform": "OTHER",
            "charge_items": [
                {
                    "charge_item_external_id": "CHXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                    "charge_item_group_external_id": "CIXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                    "charge_item_name": "Visa Mastercard Discover",
                    "charge_item_ref": "10011",
                    "fee_collection_type": "INTERCHANGE",
                    "charge_decimals": "2",
                    "is_invisible": "0",
                    "is_activated": "1",
                    "is_boarding_activated": "1",
                    "is_mandatory": "1",
                    "is_merged_charges": "0",
                    "charge_item_prices": [
                        {
                            "charge_item_price_charges": [
                                {
                                    "fee_type": "1",
                                    "category": "3",
                                    "minimum_perc_charge": "0.00000",
                                    "maximum_perc_charge": "0.00000",
                                    "default_perc_charge": "0.00000",
                                    "perc_charge": "0.00000"
                                },
                                {
                                    "fee_type": "2",
                                    "category": "3",
                                    "minimum_base_charge": "0.00000",
                                    "maximum_base_charge": "0.00000",
                                    "default_base_charge": "0.00000",
                                    "base_charge": "0.00000"
                                }
                            ]
                        }
                    ]
                },
                {
                    "charge_item_external_id": "CHTXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                    "charge_item_group_external_id": "CIGXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                    "charge_item_name": "AmexOptBlue",
                    "charge_item_ref": "777-1000105251",
                    "fee_collection_type": "INTERCHANGE",
                    "charge_decimals": "2",
                    "is_invisible": "0",
                    "is_activated": "1",
                    "is_boarding_activated": "1",
                    "is_mandatory": "1",
                    "is_merged_charges": "0",
                    "charge_item_prices": [
                        {
                            "charge_item_price_charges": [
                                {
                                    "fee_type": "1",
                                    "category": "3",
                                    "minimum_perc_charge": "0.00000",
                                    "maximum_perc_charge": "0.00000",
                                    "default_perc_charge": "0.00000",
                                    "perc_charge": "0.00000"
                                },
                                {
                                    "fee_type": "2",
                                    "category": "3",
                                    "minimum_base_charge": "0.00000",
                                    "maximum_base_charge": "0.00000",
                                    "default_base_charge": "0.00000",
                                    "base_charge": "0.00000"
                                }
                            ]
                        }
                    ]
                }
            ]
        },
        "package_external_id": "OPXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
        "merchant_sub_group": {
            "group_name": "SUB GROUP"
        }
    }
}
```
<!-- type: tab-end -->

---

### Adding an Online offering to an Outlet

To add the online offering, we will use the information from the equipment retrieval endpoint and add this to the outlet in an object `online_offer` in the `ADD_OUTLET` endpoint. This will need to send the service charge being used and its pricing, with an `"is_selected":"1"` . Mulitple items from an offering can be added to an outlet, and can be added alongside regular equipment offerings. 

<!--
type: tab
titles: Acquiring offer Block + Offer Package, Sample being used in ADD_APPLICATION
-->

JSON format for online offer:

```json
"online_offer": {
    "equipment_offering_external_id": "EQXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
    "selected_offer_item": null,
    "bundles": [
        {
            "equipment_bundle_external_id": "EQXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
            "equipment_bundle_item_external_id": "EBXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
            "bundle_name": "SYSTEM_GENERATED",
            "is_boarding_activated": null,
            "bundle_items": [
                {
                    "equipment_bundle_item_external_id": "EBXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                    "is_mandatory": "0",
                    "is_invisible": "0",
                    "service": {
                        "service_external_id": "PROXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                        "service_type": "VAR",
                        "service_name": "VAR",
                        "service_api_code": "XXXXX",
                        "service_for": "ECOM",
                        "service_for_group": "ONLINE_PRODUCT"
                    },
                    "service_charges": [
                        {
                            "service_charge_item_external_id": "SCXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                            "alliance_external_id": "ALLXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
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
                            "date_added": "2022-02-25 13:07:43",
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
```
---

<!-- type: tab -->

JSON sample request in `ADD_OUTLET`:

```json
{
    "request_source": {
        "initiator": "ALLIANCE",
        "alliance_code": "ALLIANCE",
    },
    "operation": {
        "operation_type": "ADD_OUTLET",
        "version": "2.0.0"
    },
    "application": {
        "application_reference": "3330XXXXXX"
    },
    "outlet": {
        "parent_mid": "7001000XXXXXXX",
        "trade_name": "outlet",
        "outlet_website": "http://netpay.co.uk",
        "pricing_type": "002",
        "store_number": "12",
        "primary_email_address": "technologi@technologi.co.uk",
        "business_zone": "B",
        "business_location": "H",
        "ground_floor": "G",
        "square_foot_count": "1",
        "number_of_building_floors": "1",
        "visitation_required": "1",
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
                "contact_title": "",
                "contact_first_name": "firstname",
                "contact_last_name": "lastname",
                "country_code": "840",
                "city": "City",
                "zip_code": "12345",
                "street_line_1": "street",
                "county_code": "CA",
                "floor": "1",
                "suite_apart_number": "1",
                "house_number": "11",
                "house_name": "housename",
                "email_address": "technologi@technologi.co.uk",
                "ent_telephone_code": "US|01",
                "telephone_number": "12345678"
            }
        ],
        "online_offer": {
            "equipment_offering_external_id": "EQOXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
            "selected_offer_item": null,
            "bundles": [
                {
                    "equipment_bundle_external_id": "EQXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                    "equipment_bundle_item_external_id": "EBIXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                    "bundle_name": "SYSTEM_GENERATED",
                    "is_boarding_activated": null,
                    "bundle_items": [
                        {
                            "equipment_bundle_item_external_id": "EBIXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                            "is_mandatory": "0",
                            "is_invisible": "0",
                            "service": {
                                "service_external_id": "PRXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                                "service_type": "VAR",
                                "service_name": "VAR Name",
                                "service_api_code": "00001",
                                "service_for": "ECOM",
                                "service_for_group": "ONLINE_PRODUCT"
                            },
                            "service_charges": [
                                {
                                    "service_charge_item_external_id": "SCXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
                                    "alliance_external_id": "ALLXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX-XXXXX",
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
                                    "date_added": "2022-02-25 13:07:43",
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
                "bank_name": "Bank Name",
                "bank_city": "Bank City",
                "country_code": "840",
                "zip_code": "21345-1234",
                "county_code": "AL",
                "street_line_1": "Street Line",
                "floor": "",
                "suite_apart_number": "",
                "province": " prov",
                "account_holder_name": "Test Account",
                "account_type": [
                    "CREDIT",
                    "DEBIT",
                    "CHARGEBACK"
                ],
                "bank_account_type": "CHECKING",
                "dda_number": "111111111111",
                "routing_number": "111111111"
            }
        ]
    }
}
```
<!-- type: tab-end -->

---


### Adding an Equipment offering to an Outlet

Similar to the online offer, we will need to add an additional object to the outlet request. Multiple pieces of equipment can be added to an outlet, and can be added alongside online offerings. We will need to add an `"equipment_offer"` block that containts the equipment offering we want to use from the offer package added on the `ADD_APPLICATION` request.


