# Offerings

## Pricing and Equipment
Exchange supports pricing and equipment added to Applications through the use of offerings and offer packages. Offerings are split into three types: Processsing, Equipment and Online. These offerings are created by the PayFac and added to an Offer Package, which can then be retrieved from the `/offering/avaliable` endpoint. Upon retrieving an Offer Package, the offerings avaliable in the package will be listed. Online and Equipment offerings can be retrieved by using the `/offering/equipment` endpoint for their full details. A selected Offering (by external ID) can have detals grabbed in order to retrieve the pricing information and equipment information.

Processing offerings (that contain transaction pricing and acquiring charges) may be retrieved by using the `/offering/processing` endpoint and providing the desired external ID. 
Processing offerings will be added to the Merchants **pricing level**, and equipment/online offerings at the outlet.

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
		"package_external_id": "TPI6B-4AEA4-34KLA-E7B5D-F81C9-58F7D-2B8E6",
		"package_name": "Example package name",
		"offer_code": "6565",
		"package_weight": "100",
		"package_channel": "3",
		"package_status": "1",
		"non_processing_flag": "0",
		"offer_code_status": "1",
		"processing_offers": [
			{
				"transaction_pricing_external_id": "TPI6B-34KLA-F81C9-B9617-08C45-6A1B1-2B8E6",
				"alliance_external_id": "DEBFF-C6C9D-CCE93-34KLA-DEBFF-C3907-6A1B1",
				"acquirer_external_id": "MAC85-34KLA-02AAF-CCE93-DEBFF-0979A-F81C9",
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
				"equipment_offering_external_id": "EQOE4-CFD68-34KLA-90849-8DD4F-DEBFF-1FE5B"
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
				"equipment_offering_external_id": "EQO85-B670A-34KLA-3DBBA-08C45-C3747-08C45"
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
        "transaction_pricing_external_id":"TPI6B-34KLA-F81C9-B9617-08C45-6A1B1-2B8E6"
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
            "charge_item_group_external_id": "CIG69-E5AB2-5F5D3-91E60-850F9-1ED7B-C4AD7",
            "alliance_external_id": "ALL87-C6C9D-E2B11-D357A-DEBFF-C3907-64955",
            "acquirer_external_id": "MAC85-E9418-02AAF-CCE93-1AADB-0979A-F81C9",
            "processing_platform": "OTHER",
            "fee_collection_type": "INTERCHANGE",
            "charge_item_group_name": "RegressionTransGroup",
            "charge_item_group_ref": "147852",
            "order_by": "2",
            "item_status": "1",
            "language_code": "en_gb",
            "date_added": "2021-06-17 17:33:50",
            "charge_items": [
                {
                    "charge_item_external_id": "CHID9-F2F62-30CBF-7C081-7B017-55BBC-990CF",
                    "alliance_external_id": "ALL87-C6C9D-E2B11-D357A-DEBFF-C3907-64955",
                    "acquirer_external_id": "MAC85-E9418-02AAF-CCE93-1AADB-0979A-F81C9",
                    "processing_platform": "OTHER",
                    "charge_item_name": "RegressionTransactionCharge",
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
                            "charge_item_external_id": "CHID9-F2F62-30CBF-7C081-7B017-55BBC-990CF",
                            "category": "1",
                            "fee_type": "2",
                            "minimum_base_charge": "10.00000",
                            "maximum_base_charge": "10.00000",
                            "default_base_charge": "10.00000",
                            "status": "1"
                        }
                    ],
                    "transaction_pricing_external_id": "TPI6B-3B10D-97EC5-B9617-E49CE-6A1B1-58F7D",
                    "charge_item_group_external_id": "CIG69-E5AB2-5F5D3-91E60-850F9-1ED7B-C4AD7",
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
                                    "transaction_pricing_external_id": "TPI6B-3B10D-97EC5-B9617-E49CE-6A1B1-58F7D",
                                    "charge_item_group_external_id": "CIG69-E5AB2-5F5D3-91E60-850F9-1ED7B-C4AD7",
                                    "charge_item_external_id": "CHID9-F2F62-30CBF-7C081-7B017-55BBC-990CF"
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
            "service_charge_item_external_id": "SCI6D-0FB58-F1900-2B425-59B03-EBF71-96934",
            "alliance_external_id": "ALL87-C6C9D-E2B11-D357A-DEBFF-C3907-64955",
            "acquirer_external_id": "MAC85-E9418-02AAF-CCE93-1AADB-0979A-F81C9",
            "service_item_name": "RegressionServiceItem",
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
            "transaction_pricing_external_id": "TPI6B-3B10D-97EC5-B9617-E49CE-6A1B1-58F7D",
            "is_activated": "1",
            "is_mandatory": "0",
            "is_invisible": "0",
            "service_item_charges": [
                {
                    "fee_type": "2",
                    "minimum_base_charge": "10.00",
                    "maximum_base_charge": "10.00",
                    "default_base_charge": "10.00",
                    "transaction_pricing_external_id": "TPI6B-3B10D-97EC5-B9617-E49CE-6A1B1-58F7D",
                    "service_charge_item_external_id": "SCI6D-0FB58-F1900-2B425-59B03-EBF71-96934"
                }
            ],
            "charges": [
                {
                    "service_charge_item_external_id": "SCI6D-0FB58-F1900-2B425-59B03-EBF71-96934",
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
