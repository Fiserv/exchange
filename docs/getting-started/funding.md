# Funding

#### On this section
This section regards models for funding that require API instructions to be sent. This does not cover the managed funding solution, as this does not require api to be sent in order for the funding process to occur and is added as a 'pricing' when boarding the Merchants for the system to process the funding automatically.

## Instructional Funding

### What is Instructional funding?

Instructional funding, allows the use of the `/funding/instruction` endpoint in order to direct funds in the instructional hold for a given merchant ID, where the merchant revenue amount and PayFac fee amount is directed by the request. 
Instructional funding also supports instructions sent through the `/funding/detailed-instruction` endpoint, where additional information can be added within an instruction through a 'details' block for reporting purposes. (details do not affect the funding, just act as information)

### Constructing the request

<!--
type: tab
titles: Instructional funding, JSON Instructional funding example
-->

The Instructional funding request will be constructed based on how the PayFac wants to fund the merchants instructional hold. If sending funding instructions daily, this request will be sent every day during the instructional funding window. The [Trade account info](?path=docs/getting-started/account-operations.md)  and [transaction operations](?path=docs/getting-started/transactions.md)  can be used to summarise the transactions and support calculating the fee amount to taken.

---

<!-- type: tab -->

JSON format for `/funding/instruction` , where `REVENUE_ACCOUNT` defines the merchant revenue recieved from Instructional hold and `FEE_ACCOUNT` definds the PayFac fee taken.

Supported accounts added to this request include:
- REVENUE_ACCOUNT
- FEE_ACCOUNT
- RESERVE_ACCOUNT (where applicable)
- SPLIT_ACCOUNT (for instructional split)

```json
{
  "merchant_id": "1121212",
  "total_amount": "1000.00",
  "currency": "USD",
  "accounts": [
    {
      "account_type": "REVENUE_ACCOUNT",
      "amount": "900.00"
    },
    {
      "account_type": "FEE_ACCOUNT",
      "amount": "100.00"
    }  
  ]
}
```

<!-- type: tab-end -->

---

## Intructional Split

### What is split funding?
Split funding allows the PayFac to direct funds from a merchant to third parties on the system. Three of the split funding solutions we offer require or allow instructions to be sent by API to facilitate funding. This page contains info for one method, Instructional split. 

### Instructional Split

Instructional Split funding extends the functionality of the `/funding/instruction` in order to facilitate the 'SPLIT' block, where the split is defined at a summary level for the processing MID, and 'non-processing' entities defined. Fees taken from the split amount will be recieved by the non-processing PayFac.

### Constructing the split instruction request

<!--
type: tab
titles: Instructional funding, JSON Instructional funding example
-->

The Instructional funding request will be constructed based on how the PayFac wants to fund the merchants instructional hold, and define splti amounts sent to non-processing merchants. If sending funding instructions daily, this request will be sent every day during the instructional funding window. The [Trade account info](?path=docs/getting-started/account-operations.md)  and [transaction operations](?path=docs/getting-started/transactions.md)  can be used to summarise the transactions and support calculating the fee amount to taken and to define the split.

---

<!-- type: tab -->

JSON format for `/funding/instruction` , where `REVENUE_ACCOUNT` defines the merchant revenue recieved from Instructional hold and `FEE_ACCOUNT` defines the PayFac fee taken and `SPLIT_ACCOUNT` is used to define the split amounts send to third parties. The `"split_details"` can direct funds to multiple third parties on the system, where the mid used `merchant_id` will be the `internal_mid` of the entity on the system. 

Supported accounts added to this request include:
- REVENUE_ACCOUNT
- FEE_ACCOUNT
- RESERVE_ACCOUNT (where applicable)
- SPLIT_ACCOUNT (for instructional split)

```json
{
  "merchant_id": "1121212",
  "total_amount": "1100.00",
  "currency": "USD",
  "accounts": [
    {
      "account_type": "REVENUE_ACCOUNT",
      "amount": "950.00"
    },
    {
      "account_type": "FEE_ACCOUNT",
      "amount": "100.00"
    },
    {
      "account_type": "SPLIT_ACCOUNT",
      "amount": "0.00",
      "split_details": [
        {
          "total_amount": "50.00",
          "merchant_id": "700100000006327",
          "accounts": [
            {
              "account_type": "REVENUE_ACCOUNT",
              "amount": "25.00"
            },
            {
              "account_type": "FEE_ACCOUNT",
              "amount": "25.00"
            }
          ]
        }
      ]
    }
  ]
}
```

<!-- type: tab-end -->

---
