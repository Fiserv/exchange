# Funding

This section explores instructions that can be sent by API for funding. This primarily focuses on instructional funding, however adjustment instructions and Gross/Net fee billing can occur in addition to standard managed funding.

## Instructional Funding

### What is Instructional funding?

<!-- !align: center -->
![<img src="instructional_timeline.png" width="600"/>](/assets/images/instructional_timeline.png)

Instructional funding, allows the use of the `/funding/instruction` endpoint in order to direct funds in the instructional hold for a given merchant ID, where the merchant revenue amount and PayFac fee amount is directed by the request. 
Instructional funding also supports instructions sent through the `/funding/detailed-instruction` endpoint, where additional information can be added within an instruction through a 'details' block for reporting purposes. (details do not affect the funding, just act as information)

## Process flow 

A standard daily instructional funding cycle requires the user to check through virtual account balances, check transactions, send instructions during the instructional hold window, and then reconcile using settlement endpoints and any other additional reconciliation required. A standard cycle will look similar to the below process diagram, where the instructions are actioned on item 4 below.
<!-- !align: center -->
![<img src="instruction_sequence.png" width="400"/>](/assets/images/instruction_sequence.png)

### Blocks supported in the API

The instructional API supports different scenarios for funding by using the different blocks in the request. Below is the behaviour of each block, with some examples on how this can be used.

#### Funding

The funding block is used to instruct amounts where the source of the instruction is the instructional hold, primarily used for NET funding. 
In the below example for Net funding, we include the Revenue, Chargeback, and Fee in the funding block to achieve a NET scenario.
Chargeback Validation will check that the chargeback account can support this amount being taken.

The account types affect what action is taken on the account.
For the funding block:
<ul>
  <li> type: CREDIT - Credits the specified account from the available instructional hold balance./li>
  <li> type: DEBIT - Credits the instructional hold balance from the specified account. This cannot be used to bring the instructional hold to a balance greater than it was before unless it is negative.</li>
</ul>


##### Request:

<!-- theme: success -->
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

For the billing block:
<ul>
  <li> type: CREDIT - Credits the specified amount, debiting from the submerchant (will net out for service fess configured for NET)
  <li> type: DEBIT - Not supported for the Billing block
</ul>



<!--
type: tab
titles: Gross Billing Example, Ahdoc Billing Example
-->

Please see two examples by switching the tab,  on how the billing block can be used. This sample shows how the billing block can be used to bill for a gross instruction. 

##### Request:

<!-- theme: success -->
>**IH Balance: 100**

```json
{
    "merchant_id": "520000000321",
    "currency": "USD",
    "funding": [
        {
            "account_type": "REVENUE",
            "amount": "78.30",
            "type": "CREDIT"
        }
    ],
    "billing": [
        {
            "account_type": "GROSS_FEE",
            "amount": "5.10",
            "type": "CREDIT"
        }
    ]
}   

```

<!-- type: tab -->

Example on how a submerchant could be billed an additional amount, outside of what is in the instructional hold.



##### Request:

<!-- theme: success -->
>**IH Balance: 0**

```json
{
    "merchant_id": "520000000321",
    "currency": "USD",
    "billing": [
        {
            "account_type": "GROSS_FEE",
            "amount": "15.00",
            "type": "CREDIT"
        }
    ]
}
```

<!-- type: tab-end -->

#### Chargeback

The Chargeback block is used to support recouping a chargeback amount, and debit the submerchant as part of a gross instruction.
Validation will check that the chargeback account can support this amount being taken.

For the Chargeback block:
<ul>
  <li> type: CREDIT - Recoups a chargeback amount to the Aggregator
  <li> type: DEBIT -  Reimbursing a chargeback reversal to the submerchant
</ul>

<!--
type: tab
titles: Debit Chargeback Example, Gross Reversal Example
-->

Please see two examples by switching the tab, on how the chargeback block can be used. This sample shows how the chargeback block can be used to debit the chargeback amount on top of a standard Net instruction

##### Request:

<!-- theme: success -->
>**IH Balance: 100**
<!-- theme: danger -->
>**CB Account Balance: 10.50** 

```json
{
  "merchant_id": "520000000321",
  "currency": "USD",
  "funding": [
    {
      "account_type": "REVENUE",
      "amount": "95.00",
      "type": "CREDIT"
    },
    {
      "account_type": "FEE",
      "amount": "5.00",
      "type": "CREDIT"
    }
  ],
  "chargeback": [
    {
      "account_type": "CHARGEBACK",
      "amount": "10.50",
      "type": "CREDIT"
    }
  ]
}


```

<!-- type: tab -->

Example on how a chargeback reversal can be credited back to the submerchant in a gross instruction.

##### Request:

<!-- theme: success -->
>**IH Balance: 100**
<!-- theme: danger -->
>**CB Account Balance: -10** 


```json
{
  "merchant_id": "520000000321",
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
      "account_type": "GROSS_FEE",
      "amount": "5.00",
      "type": "CREDIT"
    }
  ],
  "chargeback": [
    {
      "account_type": "CHARGEBACK",
      "amount": "10.00",
      "type": "DEBIT"
    }
  ]
}

```

<!-- type: tab-end -->

#### Adjustment

Accounts block for adjustments, primarily used for adjusting amounts in the system, after the instruction or movement has been made to move the amount into Revenue, Fee or Hold. This block may also be used in Auto funding scenarios. Description is required to be provided.

Must have two accounts specified, where one is a type CREDIT and one a type DEBIT of the same amounts.

For the Adjustment block:
<ul>
  <li> type: CREDIT - Adjusts the amount to this account.
  <li> type: DEBIT -  Adjusts the amount from this account.
</ul>

##### Request:

<!-- theme: success -->
>**Revenue Account Balance: 20**
<!-- theme: danger -->
>**Fee Account Balance: 2** 


```json
{
  "merchant_id": "520000000321",
  "currency": "USD",
  "adjustment": [
    {
      "account_type": "REVENUE",
      "amount": "15.00",
      "type": "CREDIT",
      "description": "Monthly Fee Adjustment"
    },
    {
      "account_type": "FEE",
      "amount": "15.00",
      "type": "DEBIT",
      "description": "Monthly Fee Adjustment"
    }
  ]
}

```
### Negative Instructional Hold Balances

A negative instructional hold balance that is left in the instructional hold account when the window closes will be debited from the responsible party. 
The responsible party by default is the Aggregator. If an instruction is made to make the account whole before the window closes, the responsible party will not be debited.

### Constructing the request

<!--
type: tab
titles: Instructional funding, JSON Instructional funding example
-->

The Instructional funding request will be constructed based on how the PayFac wants to fund the sub-merchants instructional hold. If sending funding instructions daily, this request will be sent every day during the instructional funding window. The [Trade account info](?path=docs/getting-started/account-operations.md)  and [transaction operations](?path=docs/getting-started/transactions.md) can be used to summarise the transactions and support calculating the fee amount to taken. The request is grouped by three types of money movement - Funding, Billing, and Chargeback. These all have their own respective accounts that can be sent as credits, debits, and split.

| Category    | Key                 | Description                                         |
|-------------|---------------------|-----------------------------------------------------|
| FEE         | FEE_ACCOUNT         | Account used to send amounts to the fee account. Funds moved to Fee will be credited to the Aggregators Operating account            |
| REVENUE     | REVENUE_ACCOUNT     | Account used to send amounts to the submerchants Revenue account. Funds moved here will be credited to the submerchant.  |
| CHARGEBACK  | CHARGEBACK_ACCOUNT     | Account used for instructing chargeback amounts. Specifying type chargeback will used the Chargeback account balance to validate the instruction and use the chargeback bank account collected on the submerchant. |
| SPLIT       | SPLIT_ACCOUNT       | Account used to split funds to third parties on the system.  |
| RESERVE     | RESERVE_ACCOUNT     | Account used to move funds into a reserve account, for release or deduction in the future. |

<!-- type: tab -->

JSON format for `/funding/instruction` , where `REVENUE_ACCOUNT` defines the merchant revenue received from Instructional hold and `FEE_ACCOUNT` defines the PayFac fee taken.

Supported accounts added to this request include:

| Category    | Key                 | Description                                         |
|-------------|---------------------|-----------------------------------------------------|
| FEE         | FEE_ACCOUNT         | Account used to send amounts to the fee account. Funds moved to Fee will be credited to the Aggregators Operating account            |
| REVENUE     | REVENUE_ACCOUNT     | Account used to send amounts to the submerchants Revenue account. Funds moved here will be credited to the submerchant.  |
| CHARGEBACK  | CHARGEBACK_ACCOUNT     | Account used for instructing chargeback amounts. Specifying type chargeback will used the Chargeback account balance to validate the instruction and use the chargeback bank account collected on the submerchant. |
| SPLIT       | SPLIT_ACCOUNT       | Account used to split funds to third parties on the system.  |
| RESERVE     | RESERVE_ACCOUNT     | Account used to move funds into a reserve account, for release or deduction in the future. |

##### Request:

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


## Responses

The response of the instructional funding API will report the movement from the instructions that were sent. This will include the current values of the accounts after the instruction. So if the instruction impacts the `Instructional Hold Account` for example, the response will provide the new balance after the instruction.

#### Example Request: 

<!-- theme: success -->
>**IH Balance: 200**

```json
{
  "merchant_id": "322543210001",
  "currency": "USD",
  "funding": [
    {
      "account_type": "FEE",
      "amount": "3.50",
      "type": "CREDIT"
    },
    {
      "account_type": "REVENUE",
      "amount": "130.00",
      "type": "CREDIT"
    } 
  ]
}
```
#### Example Response:

```json
{
    "result": "SUCCESS",
    "summary": {
        "accounts": [
            {
                "account_type": "INSTRUCTIONAL_HOLD_ACCOUNT",
                "balance": "66.50"
            },
            {
                "account_type": "FEE",
                "balance": "3.50"
            },
            {
                "account_type": "REVENUE",
                "balance": "130.00"
            }
        ],
        "instruction_tracker": ""
    }
}
```

<!-- type: row -->

<!-- type: card
title: See Net Funding
description: Funding instructions are sent as net, for a single overall settlement to the submerchant.
link: ../docs/getting-started/getting-started-instfunding-net.md
-->
<!-- type: card
title: See Gross Funding
description: Funding instructions that are sent as gross, for a single Credit and Single debit to the submerchant
link: ../docs/getting-started/getting-started-instfunding-gross.md
-->

<!-- type: card
title: See Transaction Instructions
description: Submit instructions per transaction on settlement or auth
link: ../docs/getting-started/getting-started-instfunding-split.md
-->
<!-- type: row-end -->
