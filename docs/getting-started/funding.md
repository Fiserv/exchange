# Funding
#### On this section
This section regards models for funding that require API instructions to be sent. This does not cover the managed funding solution, as this does not require api to be sent in order for the funding process to occur and is added as a 'pricing' when boarding the Merchants for the system to process the funding automatically.

## Instructional Funding
### What is Instructional funding?

Instructional funding, allows the use of the `/funding/instruction` endpoint in order to direct funds for a given merchant ID, where the merchant revenue amount and PayFac fee amount is directed by the request. 
Instructional funding also supports instructions sent through the `/funding/detailed-instruction` endpoint, where additional information can be added within an instruction through a 'details' block for reporting purposes. (details do not affect the funding, just act as information)

## Split Funding - Instructional Split and by Transaction

### What is split funding?
Split funding allows the PayFac to direct funds from a merchant to third parties on the system. Three of the split funding solutions we offer require or allow instructions to be sent by API to facilitate funding. 

### Instructional Split

Instructional Split funding extends the functionality of the `/funding/instruction` in order to facilitate the 'SPLIT' block, where the split is defined at a summary level for the processing MID, and 'non-processing' entities defined. Fees taken from the split amount will be recieved by the non-processing PayFac.

### Instructional Split by Transaction

Instructional Split by transaction requires the instructions to be sent through the `/split/transaction-details` endpoint, where the request is sent on a transaction-by-transaction basis that must contain identifiers for Exchange to identify the transaction. The split can define how each Sale, Refund and Chargeback is funded and to which MID.

<!--
type: tab
titles: Required split identifiers, JSON Split details example
-->

Minimum grid of identifiers required for definined a split using `/split/transaction-details` , where Case number refers to instructing Chargebacks amounts.

|  | Transaction Date | Transaction ID | Auth Code | Invoice ID | Case Number |
| ----------- | ----------- | ----------- | ----------- | ----------- | ----------- |
| Tranasction Date | ✔️ | ✔️ | ✔️ | ✔️ |  |
| Transaction ID | ✔️ | ✔️ |  |  |  |
| Auth Code | ✔️ |  | ✔️ | ✔️ |  |
| Invoice ID | ✔️ |  | ✔️ | ✔️ |  |
| Case Number | ✔️ |  |  | ✔️ | ✔️ |


---

<!-- type: tab -->

JSON format for `/split/transactions-details` , where `transaction_type` defines what type of transaction is being instructed:
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

### Managed Split by Transaction

Managed split by transaction also uses the `/split/transactions-details` to instruct the funding, but allows for pricing to be added at the Merchants level like the usual managed funding solution in order for the system to calculate the fees. Again, the request is sent on a transaction-by-transaction basis that must contain identifiers for Exchange to identify the transaction. The split can define how each Sale, Refund and Chargeback is funded and to which MID.

<!--
type: tab
titles: Required split identifiers, JSON Split details example
-->

Minimum grid of identifiers required for definined a split using `/split/transaction-details` , where Case number refers to instructing Chargebacks amounts.

|  | Transaction Date | Transaction ID | Auth Code | Invoice ID | Case Number |
| ----------- | ----------- | ----------- | ----------- | ----------- | ----------- |
| Tranasction Date | ✔️ | ✔️ | ✔️ | ✔️ |  |
| Transaction ID | ✔️ | ✔️ |  |  |  |
| Auth Code | ✔️ |  | ✔️ | ✔️ |  |
| Invoice ID | ✔️ |  | ✔️ | ✔️ |  |
| Case Number | ✔️ |  |  | ✔️ | ✔️ |


---

<!-- type: tab -->

JSON format for `/split/transactions-details` , where `transaction_type` defines what type of transaction is being instructed:
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
