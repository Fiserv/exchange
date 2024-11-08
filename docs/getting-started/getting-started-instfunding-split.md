---
tags: [Getting Started, Funding, Split-Funding]
---

# Split Funding

## What is Split Funding?

Split funding allows the Aggregator to split funds from a processing sub-merchant to third parties on the system. Split funding solutions can be done by instructions by API at a summary, transaction or per auth level. Please see the relevant section for each method. 

## Summary Level Splits

Instructional Split funding extends the functionality of the `/funding/instruction` in order to allow a 'split_details' block, where the split is defined at a summary level for the processing MID, and 'non-processing' entities defined. Fees taken from the split amount will be received by the non-processing PayFac.

### Constructing the Split Instruction Request

<!--
type: tab
titles: Split Instructional Funding, JSON Instructional Funding example
-->

The Instructional funding request will be constructed based on how the PayFac wants to fund the proessing merchants instructional hold, and define split amounts sent to non-processing merchants. If sending funding instructions daily, this request will be sent every day during the instructional funding window. The [Trade account info](?path=docs/getting-started/account-operations.md) and [transaction operations](?path=docs/getting-started/transactions.md) can be used to summarise the transactions and support calculating the fee amount to taken and to define the split.

---

<!-- type: tab -->

JSON format for `/funding/instruction` , where `REVENUE_ACCOUNT` defines the merchant revenue received from Instructional hold and `FEE_ACCOUNT` defines the PayFac fee taken and `SPLIT_ACCOUNT` is used to define the split amounts sent to third parties. The `"split_details"` block can direct funds to multiple third parties on the system, where the mid used `merchant_id` will be the `internal_mid` of the third party on the system. 

Supported accounts added to this request include:

| Category    | Key                 | Description                                         |
|-------------|---------------------|-----------------------------------------------------|
| FEE         | FEE_ACCOUNT         | Account used to send amounts to the fee account. Funds moved to Fee will be credited to the Aggregators Operating account            |
| REVENUE     | REVENUE_ACCOUNT     | Account used to send amounts to the sub-merchant's Revenue account. Funds moved here will be credited to the sub-merchant.  |
| CHARGEBACK  | CHARGEBACK_ACCOUNT     | Account used for instructing chargeback amounts. Specifying type chargeback will used the Chargeback account balance to validate the instruction and use the chargeback bank account collected on the sub-merchant. |
| SPLIT       | SPLIT_ACCOUNT       | Account used to split funds to third parties on the system.  |
| RESERVE     | RESERVE_ACCOUNT     | Account used to move funds into a reserve account, for release or deduction in the future. |

```json

{
  "merchant_id": "400000000005",
  "currency": "USD",
  "funding": [
    {
      "account_type": "REVENUE",
      "amount": "100.00",
      "split_details": [
        {
          "merchant_id": "400000000005",
          "accounts": {
            "account_type": "REVENUE",
            "amount": "50.00",
            "type": "CREDIT"
          }
        }
      ],
      "type": "CREDIT"
    }
  ],
  "billing": [
    {
      "account_type": "SERVICE_FEE",
      "amount": "5.00",
      "type": "CREDIT"
    }
  ],
  "chargeback": [
    {
      "account_type": "CHARGEBACK",
      "amount": "25.00",
      "type": "DEBIT"
    }
  ]
}

```

<!-- type: tab-end -->

## Transaction Level

Instructional Split by transaction requires the instructions to be sent through the `/transaction-instruction/transaction-details` endpoint, where the request is sent on a transaction-by-transaction basis that must contain identifiers for Exchange to identify the transaction. The split can define how each Sale, Refund and Chargeback is funded and to the defined MID.

This is accompanied by the `/transaction-instruction/status` endpoint in order to check the funding status of a MIDs transaction and for its involved entities

If the `/transaction-instruction/transaction-details` request has incorrect identifiers, the amounts not instructed will be held in the sub-merchants Hold account for reprocessing using  `/transaction-instruction/transaction-details` again with the correct information.

<!--
type: tab
titles: Required Split Identifiers, JSON Split Details Example
-->

Minimum grid of identifiers required for definined a split using `/transaction-instruction/transaction-details` , where Case number refers to instructing Chargebacks amounts.

|  | Transaction Date | Transaction ID | Auth Code | Invoice ID | Case Number |
| ----------- | ----------- | ----------- | ----------- | ----------- | ----------- |
| Tranasction Date | ✔️ | ✔️ | ✔️ | ✔️ |  |
| Transaction ID | ✔️ | ✔️ |  |  |  |
| Auth Code | ✔️ |  | ✔️ | ✔️ |  |
| Invoice ID | ✔️ |  | ✔️ | ✔️ |  |
| Case Number | ✔️ |  |  | ✔️ | ✔️ |


---

<!-- type: tab -->

JSON format for `transaction-instruction/transaction-details` , where `transaction_type` defines what type of transaction is being instructed:
- `transaction_type` = 1 Sale
- `transaction_type` = 2 Refund
- `transaction_type` = 3 Chargeback 

```json
{
    "processing_merchant_id": "2022XXXXXX", 
    "amount": "60.00", 
    "currency": "USD",
    "transaction_type": "1",
    "transaction_date": "2022-02-09",
    "authorization_code": "0013XXX",
    "invoice_id": "6900XXXX",
    "split_details": [
        {
            "amount": "20.00",
            "merchant_id": "2022XXXXXX"
        },
        {
            "amount": "10.00",
            "merchant_id": "7099000XXXXXX" 

        },
        {
            "amount": "10.00",
            "merchant_id": "70990XXXXXX" 

        },
        {
            "amount": "10.00",
            "merchant_id": "9849XXXXXX" 
        },
        {
            "amount": "10.00",
            "merchant_id": "98497XXXXX" 
        }
    ]
}
```

<!-- type: tab-end -->

---

### Auto-Funding Split by Transaction

Splits on a transaction level can also be done through Auto-Funding, where pricing would be added to split a percentage or amount to a third party on the system. 

## Split on Auth

Split on auth allows users through Commerce Hub to submit instructions to split money on authorized amounts. These are then settled to their respective parties through Exchange.
For split on auth info through Commerce Hub, please see documentation [here](https://developer.fiserv.com/product/CommerceHub/docs/?path=docs/Resources/Guides/Partners/PFAC/Split-Settlement.md&branch=main)



