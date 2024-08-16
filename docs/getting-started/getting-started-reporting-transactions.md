---
tags: [Getting Started, Reporting, Transactions, Chargebacks, Auto funding]
---

# Transactions in Exchange

Exchange processes transactions daily, making them available in our reporting APIs. These transactions flow into the [virtual accounts](../docs/getting-started/getting-started-reporting.md) if funding is conducted through Exchange. You can access them via the `/transaction/...` endpoints visible on the [API Explorer](../api/?type=post&path-/transaction). The field `date_added` indicates the date the transaction was added to our system.

## Requests

A 'query' can be created by adjusting the database operator and values being searched for:
```
{
    "location_id": {
        "operator": "EQ",
        "value": "202205290001"
    },
    "date_added": {
        "operator": "EQ",
        "value": "2022-05-16"
    }
}
```
This can be extended with other operators and values viewable on the [API Explorer](../api/?type=post&path-/transaction).

## Transactions

<!-- theme: info -->
>**POST** `/transaction`

Transactions include sales and refunds that are captured.

<!--
type: tab
titles: Request , Response 
-->
#### Request: 

```json

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
<!-- type: tab -->

#### Response:

```json
{
  "result": "SUCCESS",
  "response": {
    "limit": "5",
    "page": "1",
    "summary_status": "FOUND",
    "transactions": [
      {
        "_id": "6f2522147afbba675c",
        "processed_currency_code": "840",
        "submerchant_id": "00052606609801",
        "card_type": "00001",
        "reject_indicator": "N",
        "transaction_amount": "10",
        "transaction_id": "6669800004321",
        "airline_ticket_number": "",
        "auth_source": "",
        "authorization_amount": "10",
        "reference_number": "66998669893214321000001",
        "authorization_code": "0000AB",
        "authorization_date": "2021-11-01",
        "authorization_response_code": "00",
        "authorization_sic_code": "5000",
        "avs_flag": "Z",
        "bank_reference_number": "",
        "batch_date": "2021-11-01",
        "batch_number": "666989800001",
        "card_number": "XXXXXXXXXXXX4321",
        "card_presence_indicator": "1",
        "cardholder_id_method": "",
        "cat_level": "",
        "currency_conversion_rate": "0.000000000",
        "cvc2_result": "",
        "cvv2_result": "",
        "entry_mode": "01",
        "expiration_date": "1022",
        "external_id": "",
        "funded_date": "2021-11-01",
        "health_care_card": "",
        "invoice_id": "54321669898",
        "location_dba_name": "MMISTest DBA NAME",
        "market_specific_indicator": "",
        "mc_cardholder_authentication": "",
        "mc_security_protocol": "",
        "merchant_reference_number": "32100000",
        "mobile_indicator": "",
        "partial_auth_indicator": "",
        "pc_terminal_capability": "",
        "pinless_debit": "N",
        "reject_reason": "",
        "response_code": "",
        "soft_descriptor": "ABC*MMISTest LEGAL",
        "split_details": [
          {
            "processing_fee": "0.0100",
            "hold_flag": "STORE_SPLIT",
            "txm_unique_id": "-52606609801-52606609801",
            "amount": "10.00",
            "source_merchant_id": "52606609801",
            "target_merchant_id": "52606609801",
            "source_node_id": "20000",
            "target_hierarchy_type": "1",
            "target_node_id": "20000"
          }
        ],
        "store_number": "01",
        "submitted_currency_amount": "10",
        "submitted_currency_code": "840",
        "terminal_id": "54321",
        "total_auth_amount": "10",
        "transaction_date": "2021-11-01",
        "transaction_integrity_class": "",
        "transaction_mode": "A",
        "transaction_source": "A",
        "transaction_status": "A",
        "transaction_time": "20:30:00",
        "transaction_type": "3",
        "usage_indicator": "A",
        "visa_chip_condition_code": "",
        "visa_purchase_identifier": "",
        "visa_purchase_identifier_format": "1",
        "visa_service_develop": "1",
        "location_id": "52606609801",
        "merchant_node_id": "20000",
        "pfac_node_id": "10",
        "outlet_id": "10000",
        "alliance_id": "16000000",
        "merchant_id": "6000",
        "plan_code": "VABC",
        "reclass_code": "",
        "record_type": "CREDIT_DETAIL_FUNDED",
        "hierarchy_id": "52606609801",
        "hierarchy_level_no": "10",
        "date_added": "2021-11-01",
        "surcharge_indicator": "",
        "surcharge_amount": "0",
        "special_reference_1": "",
        "special_reference_2": "",
        "user_data_2": ""
      }
    ]
  }
}
```
<!-- type: tab-end -->

## Rejects

<!-- theme: info -->
>**POST** `/transaction/rejects`

Rejected transactions are separated into the rejects endpoint.

<!--
type: tab
titles: Request , Response 
-->
#### Request: 

```json

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
<!-- type: tab -->

#### Response:

```json
{
  "result": "SUCCESS",
  "response": {
    "limit": "5",
    "page": "1",
    "summary_status": "FOUND",
    "transactions": [
      {
        "_id": "6f2522147afbba675c",
        "processed_currency_code": "840",
        "submerchant_id": "00052606609801",
        "card_type": "00001",
        "reject_indicator": "Y",
        "transaction_amount": "10",
        "transaction_id": "6669800004321",
        "airline_ticket_number": "",
        "auth_source": "",
        "authorization_amount": "10",
        "reference_number": "66998669893214321000001",
        "authorization_code": "0000AB",
        "authorization_date": "2021-11-01",
        "authorization_response_code": "00",
        "authorization_sic_code": "5000",
        "avs_flag": "Z",
        "bank_reference_number": "",
        "batch_date": "2021-11-01",
        "batch_number": "666989800001",
        "card_number": "XXXXXXXXXXXX4321",
        "card_presence_indicator": "1",
        "cardholder_id_method": "",
        "cat_level": "",
        "currency_conversion_rate": "0.000000000",
        "cvc2_result": "",
        "cvv2_result": "",
        "entry_mode": "01",
        "expiration_date": "1022",
        "external_id": "",
        "funded_date": "2021-11-01",
        "health_care_card": "",
        "invoice_id": "54321669898",
        "location_dba_name": "MMISTest DBA NAME",
        "market_specific_indicator": "",
        "mc_cardholder_authentication": "",
        "mc_security_protocol": "",
        "merchant_reference_number": "32100000",
        "mobile_indicator": "",
        "partial_auth_indicator": "",
        "pc_terminal_capability": "",
        "pinless_debit": "N",
        "reject_reason": "29 - INVALID TRANSACTION AMOUNT",
        "response_code": "",
        "soft_descriptor": "ABC*MMISTest LEGAL",
        "store_number": "01",
        "submitted_currency_amount": "10",
        "submitted_currency_code": "840",
        "terminal_id": "54321",
        "total_auth_amount": "10",
        "transaction_date": "2021-11-01",
        "transaction_integrity_class": "",
        "transaction_mode": "A",
        "transaction_source": "A",
        "transaction_status": "A",
        "transaction_time": "20:30:00",
        "transaction_type": "3",
        "usage_indicator": "A",
        "visa_chip_condition_code": "",
        "visa_purchase_identifier": "",
        "visa_purchase_identifier_format": "1",
        "visa_service_develop": "1",
        "location_id": "52606609801",
        "merchant_node_id": "20000",
        "pfac_node_id": "10",
        "outlet_id": "10000",
        "alliance_id": "16000000",
        "merchant_id": "6000",
        "plan_code": "VABC",
        "reclass_code": "",
        "record_type": "CREDIT_DETAIL_FUNDED",
        "hierarchy_id": "52606609801",
        "hierarchy_level_no": "10",
        "date_added": "2021-11-01",
        "surcharge_indicator": "",
        "surcharge_amount": "0",
        "special_reference_1": "",
        "special_reference_2": "",
        "user_data_2": ""
      }
    ]
  }
}

```
<!-- type: tab-end -->

## Chargeback Adjustments

<!-- theme: info -->
>**POST** `/transaction/chargeback-adjustments`

Chargeback Adjustments report actual financial adjustments related to a chargeback. This can be used in a fund-the-PFAC setup to know when a chargeback needs to be recouped or reimbursed from a sub-merchant.  

<!--
type: tab
titles: Request , Response 
-->
#### Request: 

```json

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
<!-- type: tab -->

#### Response:

```json
{
  "result": "SUCCESS",
  "response": {
    "limit": "5",
    "page": "1",
    "summary_status": "FOUND",
    "chargeback_adjustments": [
      {
        "_id": "ddss9eebae9565aeeb",
        "alliance_id": "16000200",
        "pfac_node_id": "10",
        "merchant_id": "2000",
        "merchant_node_id": "8000",
        "outlet_id": "3000",
        "location_id": "526232132199",
        "date_added": "2021-11-10",
        "record_type": "ADJUSTMENT_DETAIL",
        "hierarchy_id": "526232000099",
        "hierarchy_level_no": "10",
        "location_dba_name": "MMISTest DBA NAME",
        "store_number": "",
        "external_id": "",
        "funded_date": "2021-11-01",
        "processed_date": "2021-11-01",
        "currency_code": "840",
        "dda_number": "XXXXX321",
        "aba_number": "XXXXX6699",
        "adjustment_date": "2021-11-01",
        "fee_details": [
          {
            "fee_amount": "0.4500",
            "charge_item_external_id": "CHIC23-A1AC5-A1AC5-30LC5-30LC5-3657B-3657B",
            "charge_item_type": "CHARGE",
            "charge_item_name": "Chargeback Fee",
            "charge_item_ref": "CB001",
            "fee_collection_type": "BLENDED",
            "item_charge_breakdown": [
              {
                "fee_type": "2",
                "fee_amount": "15.00000",
                "unit_charge": "15.00"
              }
            ]
          }
        ],
        "card_type": "00001",
        "adjustment_code": "CB",
        "adjustment_description": "REVERSALS",
        "adjustment_amount_sign": "+",
        "adjustment_amount": "10.30",
        "adjustment_type": "C",
        "invoice_date": "2021-11-01",
        "adjustment_invoice_number": "3339866669001",
        "batch_number": "666933221",
        "card_number": "XXXXXXXXXXXX6699",
        "chargeback_code": "1000",
        "case_number": "666993321001",
        "bank_reference_number": "",
        "sds_reference_number": "",
        "new_adjustment_description": "REVERSALS",
        "transaction_count": "0",
        "rate": "0.000000",
        "unit_amount": "0.00",
        "submit_date": "2021-11-01",
        "special_reference_1": ""
      }
    ]
  }
}


```
<!-- type: tab-end -->

## Chargebacks

<!-- theme: info -->
>**POST** `/transaction/chargebacks`

Reports the details on the chargeback case. Can be linked to the chargeback adjustments using the invoice number.

<!--
type: tab
titles: Request , Response 
-->
#### Request: 

```json

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
<!-- type: tab -->

#### Response:

```json
{
  "result": "SUCCESS",
  "response": {
    "limit": "5",
    "page": "1",
    "summary_status": "FOUND",
    "chargebacks": [
      {
        "_id": "djjaee4cce8de5jae",
        "alliance_id": "16000001",
        "pfac_node_id": "10",
        "merchant_id": "2000",
        "merchant_node_id": "8000",
        "outlet_id": "3000",
        "location_id": "526232132199",
        "date_added": "2021-11-01",
        "record_type": "CHARGEBACK_DETAIL",
        "hierarchy_id": "526232000099",
        "hierarchy_level_no": "10",
        "location_dba_name": "MMISTest DBA NAME",
        "store_number": "",
        "external_id": "",
        "dispute_type": "Pre-Arbitration",
        "request_type": "F",
        "status_date": "2021-11-01",
        "status_description": "REVERSED",
        "request_date": "2021-11-01",
        "chargeback_currency_code": "840",
        "dispute_amount_sign": "+",
        "dispute_amount": 10.3,
        "reason_code": "1000",
        "reason_code_description": "Fraud",
        "ids_case_number": "669949966001",
        "acquirer_reference_number": "666989832100000111",
        "chargeback_cycle": "I",
        "first_chargeback_date": "2021-11-01",
        "card_type": "00001",
        "card_number": "XXXXXXX6699",
        "exp_date": "",
        "adjustment_date": "2021-11-01",
        "transaction_date": "2021-11-01",
        "batch_date": "2021-11-01",
        "batch_number": "6669999321",
        "processed_transaction_currency_code": "840",
        "processed_transaction_amount_sign": "+",
        "processed_transaction_amount": "10.30",
        "authorization_code": "AB001D",
        "invoice_number": "66698989",
        "airline_ticket_number": "",
        "sic_code": "0001",
        "receive_date": "20211011",
        "adjustment_amount_sign": "+",
        "adjustment_amount": "10.30",
        "submerchant_id": "000526333132199",
        "soft_descriptor": "ABC*MMISTest Business",
        "submitted_transaction_currency_code": "840",
        "submitted_transaction_amount_sign": "+",
        "submitted_transaction_amount": "10.30",
        "transaction_service_code": "0",
        "transaction_pos_entry_mode": "01",
        "work_type": "",
        "loan_number": "",
        "work_order_number": "",
        "mobile_indicator": "",
        "special_reference_2": "",
        "user_data_2": ""
      }
    ]
  }
}

```
<!-- type: tab-end -->

## Authorizations

<!-- theme: info -->
>**POST** `/transaction/authorizations`

Reports authorizations being loaded into the system, typically every 15 minutes.

<!--
type: tab
titles: Request , Response 
-->
#### Request: 

```json

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
<!-- type: tab -->

#### Response:

```json
{
  "result": "SUCCESS",
  "response": {
    "limit": "1",
    "page": "1",
    "summary_status": "FOUND",
    "authorizations": [
      {
        "_id": "617ce27ea722d2997ce",
        "alliance_id": "16000200",
        "pfac_node_id": "1",
        "merchant_id": "2000",
        "merchant_node_id": "8000",
        "outlet_id": "4000",
        "location_id": "52606609801",
        "date_added": "2021-11-01",
        "record_type": "AUTHORIZATION_DETAILS",
        "hierarchy_id": "52606609801",
        "hierarchy_level_no": "60",
        "location_dba_name": "MMISTest DBA Name",
        "store_number": "",
        "external_id": "",
        "currency_code": "840",
        "card_type": "00001",
        "cardholder_number": "XXXXXXXXXXXX4321",
        "expiration_date": "0122",
        "auth_amount_sign": "+",
        "auth_amount": "10.15",
        "auth_time": "09:30:15",
        "auth_date": "2021-11-01",
        "auth_code": "",
        "avs_flag": "Z",
        "response_code": "1",
        "service_code": "",
        "auth_trans_code": "",
        "aci": "N",
        "cavv_ucaf": "0",
        "mc_promotion_code": "",
        "mc_pos_data_codes": "",
        "visa_valid_code": "",
        "visa_dynamic_currency_code": "",
        "authorization_fee_sign": "",
        "authorization_fee": "",
        "network_fee_sign": "",
        "network_fee": "",
        "order_number": "43216698    0000669898",
        "auth_tracker": "43266.0010200034567",
        "settlement_status": "NOT_SETTLED",
        "user_data_2": ""
      }
    ]
  }
}

```
<!-- type: tab-end -->

## Adjustments

Reports PayFac adjustments in the system

<!-- theme: info -->
>**POST** `/transaction/adjustments`

<!--
type: tab
titles: Request , Response 
-->
#### Request: 

```json

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
<!-- type: tab -->

#### Response:

```json
{
  "result": "SUCCESS",
  "response": {
    "limit": "1",
    "page": "1",
    "summary_status": "FOUND",
    "adjustments": [
      {
        "_id": "1cffga3bba5e4724528",
        "alliance_id": "16000200",
        "pfac_node_id": "10",
        "location_id": "54321669898",
        "date_added": "2021-11-01",
        "record_type": "ADJUSTMENT_DETAIL",
        "hierarchy_id": "54321669898",
        "hierarchy_level_no": "60",
        "location_dba_name": "MMISTest DBA Name",
        "store_number": "AGENT",
        "external_id": "",
        "funded_date": "2021-11-01",
        "processed_date": "2021-11-01",
        "currency_code": "840",
        "dda_number": "XXXXX4321",
        "aba_number": "XXXXX1234",
        "adjustment_date": "2021-11-01",
        "card_type": "00002",
        "adjustment_code": "15",
        "adjustment_description": "ASSESSMENT FEE $10.00",
        "adjustment_amount_sign": "-",
        "adjustment_amount": "-0.06",
        "adjustment_type": "C",
        "invoice_date": "2021-11-01",
        "adjustment_invoice_number": "000000",
        "batch_number": "000",
        "card_number": "",
        "chargeback_code": "",
        "case_number": "00000",
        "bank_reference_number": "",
        "sds_reference_number": "",
        "new_adjustment_description": "ASSESSMENT FEE",
        "transaction_count": "1",
        "rate": "0.001200",
        "unit_amount": "10.00",
        "submit_date": "2021-11-01",
        "special_reference_1": ""
      }
    ]
  }
}

```
<!-- type: tab-end -->

## Auto-Funding Calculations

Auto Funding on Exchange performs calculations automatically based on configurations set for that sub-merchant. As this is done by the system, the calculations performed will be added to the corresponding transactions.

### Processing Fee Calculations

To retrieve calculations performed by Auto Fundings processing charges at a transaction level, the `fee_details` block in the `/transaction` , `/transaction/chargeback-adjustments`, `/transaction/rejects`  endpoints can be used. This provides a breakdown of all charge items that have applied for this charge, and how they were calculated. For full spec, please find API [here](../api/?type=post&path=/transaction)

### Service Fee Calculations

Within Auto Funding, 'service billing' can be added to a sub-merchant. This allows for the user to bill for non-transaction related charges such as a monthly charge. By calling the `/billing/fee-details` endpoint this will retrieve any service charge items that have been billed for that day. For full spec, please find API [here](../api?type=post&path=/account/billing/fee-details) 

