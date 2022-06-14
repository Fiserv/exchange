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


