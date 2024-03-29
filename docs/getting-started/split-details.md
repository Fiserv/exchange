# Instructions by Transaction

## Instructions by Transactions (Split Funding)
Split funding allows the PayFac to direct funds from a processing sub-merchant to third parties on the system. 
This page contains info for instructing by transaction.

### Split Funding - by Transaction

Instructional Split by transaction requires the instructions to be sent through the `/transaction-instruction/transaction-details` endpoint, where the request is sent on a transaction-by-transaction basis that must contain identifiers for Exchange to identify the transaction. The split can define how each Sale, Refund and Chargeback is funded and to the defined MID.

This is accompanied by the `/transaction-instruction/status` endpoint in order to check the funding status of a MIDs transaction and for its involved entities

If the `/transaction-instruction/transaction-details` request has incorrect identifiers, the amounts not instructed will be held in the sub-merchants Hold account for reprocessing using  `/transaction-instruction/transaction-details` again with the correct information.

<!--
type: tab
titles: Required split identifiers, JSON Split details example
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

Managed split by transaction also uses the `transaction-instruction/transaction-details` to instruct the funding, but allows for pricing to be added at the Merchants level like the usual managed funding solution in order for the system to calculate the fees. Again, the request is sent on a transaction-by-transaction basis that must contain identifiers for Exchange to identify the transaction. The split can define how each Sale, Refund and Chargeback is funded and to which MID.



<!--
type: tab
titles: Required split identifiers, JSON Split details example
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

The `/transaction-instruction/status` allows the user to view the status of a defined split, using the same identifiers that were used to send the initial  `/transaction-instruction/transaction-details` request.
This will respond with the current `status` of the split. Notably this can be used to see if a split has failed, and if it needs reprocessing through the  `/transaction-instruction/transaction-details` again, or if the split has been successful.
