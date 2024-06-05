# Funding

#### On this section
This section regards models for funding that require API instructions to be sent. This does not cover the managed funding solution, as this does not require api to be sent in order for the funding process to occur and is added as a 'pricing' when boarding the sub-merchants for the system to process the funding automatically.

## Instructional Funding

### What is Instructional funding?

<!-- !align: center -->
![<img src="instructional_timeline.png" width="600"/>](/assets/images/instructional_timeline.png)

Instructional funding, allows the use of the `/funding/instruction` endpoint in order to direct funds in the instructional hold for a given merchant ID, where the merchant revenue amount and PayFac fee amount is directed by the request. 
Instructional funding also supports instructions sent through the `/funding/detailed-instruction` endpoint, where additional information can be added within an instruction through a 'details' block for reporting purposes. (details do not affect the funding, just act as information)

### Blocks supported in the API

The instructional API supports different scenarios for funding by using the different blocks in the request. Below is the behaviour of each block, with some examples on how this can be used.

#### Funding

The funding block is used to instruct amounts where the source of the instruction is the instructional hold, primarily used for NET funding. 
In the below example for Net funding, we include the Revenue, Chargeback, and Fee in the funding block to achieve a NET scenario.
Chargeback Validation will check that the chargeback account can support this amount being taken.

The account types affect what action is taken on the account.
For the funding block:
`type: CREDIT` Credits the specified account from the available instructional hold balance.
`type: DEBIT` Credits the instructional hold balance from the specified account. This cannot be used to bring the instructional hold to a balance greater than it was before unless it is negative.



<!-- theme: info -->
>**IH Balance: 100** 

```json
{
  "merchant_id": "520000000321",
  "currency": "USD",
  "funding": [
    {
      "account_type": "REVENUE",
      "amount": "84.50",
      "type": "CREDIT"
    },
    {
      "account_type": "CHARGEBACK",
      "amount": "10.50",
      "type": "CREDIT"
    },
    {
      "account_type": "FEE",
      "amount": "5.00",
      "type": "CREDIT"
    }
  ]
}
```
The settlement that will generate from this instruction will be a settlement of $84.50 to the submerchant, and $15.50 to the Aggregator 

#### Billing

The billing block is used to call out specific fee amounts to be collected, and can support billing gross fees + Service fees (depending on configuration of the submerchant). This is primarily used as part of a gross instruction.

 "type": "DEBIT" -> Not supported for the Billing block
 "type:: "CREDIT" -> Credits the specified amount, debiting from the submerchant (will net out for service fess configured for NET)

```json
{
  "merchant_id": "520000000321",
  "currency": "USD",
  "funding": [
    {
      "account_type": "REVENUE",
      "amount": "84.50",
      "type": "CREDIT"
    },
    {
      "account_type": "CHARGEBACK",
      "amount": "10.50",
      "type": "CREDIT"
    },
    {
      "account_type": "FEE",
      "amount": "5.00",
      "type": "CREDIT"
    }
  ]
}
```

#### Chargeback

The Chargeback block is used to support recouping a chargeback amount, and debit the submerchant as part of a gross instruction.
Validation will check that the chargeback account can support this amount being taken.

 "type": "DEBIT" -> Reimbursing a chargeback reversal to the submerchant
 "type:: "CREDIT" -> Recoups a chargeback amount to the Aggregator

#### Adjustment

Accounts block for adjustments, primarily used for adjusting amounts in the system. This block may also be used in Auto funding scenarios. Description is required to be provided

Must have two accounts specified, where one is a type CREDIT and one a type DEBIT of the same amounts.

 "type": "DEBIT" -> Adjusts the amount from this account.
 "type": "CREDIT" -> Adjusts the amount to this account.

### Constructing the request

<!--
type: tab
titles: Instructional funding, JSON Instructional funding example
-->

The Instructional funding request will be constructed based on how the PayFac wants to fund the sub-merchants instructional hold. If sending funding instructions daily, this request will be sent every day during the instructional funding window. The [Trade account info](?path=docs/getting-started/account-operations.md)  and [transaction operations](?path=docs/getting-started/transactions.md) can be used to summarise the transactions and support calculating the fee amount to taken. The request is grouped by three types of money movement - Funding, Billing, and Chargeback. These all have their own respective accounts that can be sent as credits, debits, and split.

---

<!-- type: tab -->

JSON format for `/funding/instruction` , where `REVENUE_ACCOUNT` defines the merchant revenue received from Instructional hold and `FEE_ACCOUNT` defines the PayFac fee taken.

Supported accounts added to this request include:

| Category    | Key                 | Description                                         |
|-------------|---------------------|-----------------------------------------------------|
| FEE         | FEE_ACCOUNT         | Account used for tracking fees collected.            |
| REVENUE     | REVENUE_ACCOUNT     | Account where net revenue is recorded and tracked.  |
| CHARGEBACK  | CHARGEBACK_ACCOUNT     | Account for recording revenue related to chargebacks. |
| SPLIT       | SPLIT_ACCOUNT       | Account utilized when splitting funds for instructional purposes. |
| RESERVE     | RESERVE_ACCOUNT     | Account holding funds in reserve for contingencies. |

```json

{
  "merchant_id": "400000000005",
  "currency": "USD",
  "funding": [
    {
      "account_type": "REVENUE",
      "amount": "100.00",
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
      "amount": "250.00",
      "type": "DEBIT"
    }
  ]
}

```

<!-- type: tab-end -->

---

## Response

The response of the instructional hold API will report the movement from the instruction. 


## Process flow 

A standard daily instructional funding cycle requires the user to check through virtual account balances, check transactions, send instructions during the instructional hold window, and then reconcile using settlement endpoints and any other additional reconciliation required. A standard cycle  will look similar to the below process diagram:
<!-- !align: center -->
![<img src="instruction_sequence.png" width="400"/>](/assets/images/instruction_sequence.png)

## Instructional Split Funding

### What is split funding?
Split funding allows the PayFac to direct funds from a processing sub-merchant to third parties on the system. Three of the split funding solutions we offer require or allow instructions to be sent by API to facilitate funding. This page contains info for one method, Instructional split. 

### Instructional Split

Instructional Split funding extends the functionality of the `/funding/instruction` in order to allow a 'split_details' block, where the split is defined at a summary level for the processing MID, and 'non-processing' entities defined. Fees taken from the split amount will be received by the non-processing PayFac.

### Constructing the split instruction request

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
| FEE         | FEE_ACCOUNT         | Account used for tracking fees collected.            |
| REVENUE     | REVENUE_ACCOUNT     | Account where net revenue is recorded and tracked.  |
| CHARGEBACK  | CHARGEBACK_ACCOUNT     | Account for recording revenue related to chargebacks. |
| SPLIT       | SPLIT_ACCOUNT       | Account utilized when splitting funds for instructional purposes. |
| RESERVE     | RESERVE_ACCOUNT     | Account holding funds in reserve for contingencies. |

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

---
