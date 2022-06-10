# Funding
For solutions that require instructions to be sent, Exchange offers funding API to facilitate the funding.

# Instructional Funding

For Instructional Funding, the `/funding/instruction/` endpoint can be uesd in order to direct funds for a given merchant ID. 
Instructional funding also supports instructions sent through the `/funding/detailed-instruction/` endpoint, where additional information can be added within an instruction through a 'details' block for reporting purposes. (details do not affect the funding, just act as information)

# Split Funding - Instructional Split and by Transaction

## What is split funding?
Split funding allows the PayFac to direct funds from a merchant to third parties on the system. Three of the split funding solutions we offer require or allow instructions to be sent by API to facilitate funding. 

### Instructional Split

Instructional Split funding extends the functionality of the `/funding/instruction/` in order to facilitate the 'SPLIT' block, where the split is defined at a summary level for the processing MID, and 'non-processing' entities defined. Fees taken from the split amount will be recieved by the non-processing PayFac.

### Instructional Split by Transaction

Instructional Split by transaction requires the instructions to be sent through the `/split/transaction-details/` endpoint, where the request is sent on a transaction-by-transaction basis that must contain identifiers for Exchange to identify the transaction. The split can define how each Sale, Refund and Chargeback is funded and to which MID.

<!--
type: tab
titles: Split Identifiers, JSON Split Details Example
-->

|  | Transaction Date | Transaction ID | Auth Code | Invoice ID | Case Number |
| ----------- | ----------- | ----------- | ----------- | ----------- | ----------- |
| Tranasction Date | ✔️ | ✔️ | ✔️ | ✔️ |  |
| Transaction ID | ✔️ | ✔️ |  |  |  |
| Auth Code | ✔️ |  | ✔️ | ✔️ |  |
| Invoice ID | ✔️ |  | ✔️ | ✔️ |  |
| Case Number | ✔️ |  |  | ✔️ | ✔️ |


---

<!-- type: tab -->

JSON format for `APPLICATION_SUBMIT`:

```json
{
    "processing_merchant_id": "2022XXXXXX", 
    "amount": "60.00", 
    "currency": "USD",
    "transaction_type": "1",
    "transaction_date": "2022-02-09",
    "authorization_code": "00131P",
    "invoice_id": "69000178",
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

Instructional Split funding extends the functionality of the `/funding/instruction/` in order to facilitate the 'SPLIT' block, where the split is defined at a summary level for the processing MID, and 'non-processing' entities defined. Fees taken from the split amount will be recieved by the non-processing PayFac.
