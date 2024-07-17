
# Split Funding

## What is split funding?

Split funding allows the Aggregator to split funds from a processing sub-merchant to third parties on the system. Split funding solutions can be done by instructions by API at a summary, transaction or per auth level. Please see the relevant section for each method. 

## Instructional Split

Instructional Split funding extends the functionality of the `/funding/instruction` in order to allow a 'split_details' block, where the split is defined at a summary level for the processing MID, and 'non-processing' entities defined. Fees taken from the split amount will be received by the non-processing PayFac.

## Constructing the split instruction request

<!--
type: tab
titles: Split instructional funding, JSON instructional funding example
-->

The Instructional funding request will be constructed based on how the PayFac wants to fund the proessing merchants instructional hold, and define split amounts sent to non-processing merchants. If sending funding instructions daily, this request will be sent every day during the instructional funding window. The [Trade account info](?path=docs/getting-started/account-operations.md) and [transaction operations](?path=docs/getting-started/transactions.md) can be used to summarise the transactions and support calculating the fee amount to taken and to define the split.

---

<!-- type: tab -->

JSON format for `/funding/instruction` , where `REVENUE_ACCOUNT` defines the merchant revenue received from Instructional hold and `FEE_ACCOUNT` defines the PayFac fee taken and `SPLIT_ACCOUNT` is used to define the split amounts sent to third parties. The `"split_details"` block can direct funds to multiple third parties on the system, where the mid used `merchant_id` will be the `internal_mid` of the third party on the system. 

Supported accounts added to this request include:

| Category    | Key                 | Description                                         |
|-------------|---------------------|-----------------------------------------------------|
| FEE         | FEE_ACCOUNT         | Account used to send amounts to the fee account. Funds moved to Fee will be credited to the Aggregators Operating account            |
| REVENUE     | REVENUE_ACCOUNT     | Account used to send amounts to the submerchants Revenue account. Funds moved here will be credited to the submerchant.  |
| CHARGEBACK  | CHARGEBACK_ACCOUNT     | Account used for instructing chargeback amounts. Specifying type chargeback will used the Chargeback account balance to validate the instruction and use the chargeback bank account collected on the submerchant. |
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

## Split on Auth

Split on auth allows users through commercehub to submit instructions to split money on authorized amounts. These are then settled to their respective parties through Exchange.
For split on auth info through CommerceHub, please see documentation [here](?path=docs/Resources/Guides/Partners/PFAC/Split-Settlement.md&branch=preview#account-type)



