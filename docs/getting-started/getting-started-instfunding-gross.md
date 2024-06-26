
# Gross Instructional Funding

This section will focus on creating Funding instructions for Gross scenarios. Please refer to the main [Funding](?path=docs/getting-started/getting-started-funding.md) page first for details on the Accounts and Process flow.

## What is Gross Instructional funding?

Instructional funding allows instructions to be sent via API to the instructional hold, for fees to be delegated, and funds to be settled to the submerchant.
For Gross instructions, we will create one settlement for Credits, **and** one for debits (Where as Net funding is one overall settlement). This is primarily done by utilising the `FUNDING`, `BILLING` and `CHARGEBACK` block on the `/funding/instruction` endpoint.

## Constructing a Gross instruction 

<!-- theme: info -->
>**POST** `/funding/instruction`

The blocks in the funding instruction will specify each amount separately, rather than rolled into the funding block like Net funding. 
This means that for an instructional hold balance of 100, you would need to send the funding and billing amounts gross using their respective blocks. 
Please see below example:
<!-- theme: success -->
>**IH Balance: 100**

##### Request:

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
      "type": "CREDIT"
    }
  ]
}

```
This instruction would generate settlements of $100.00 Credit to the submerchant, $15.00 Debit to the submerchant and a Credit settlement of $15.50 to the Aggregator.

## Managing Chargeback through GROSS instructions

Chargeback is represented through virtual accounts on the system, which means there are a few options on recouping or reimbursing amounts for the chargeback through instructional funding.

The Chargeback virtual account keeps balances from Chargeback Adjustments that happen outside the system. This represents information that the chargeback has occurred, and this balance is used for validation when instruction funds with an `"account_type": "CHARGEBACK"`. There are two ways of doing this through Gross instructions, seen below.

### Using the Chargeback account

In order to use the chargeback account in the instruction, the `"account_type": "CHARGEBACK"` must be specified. This will make the instruction validate against the current Chargeback Virtual Account Balance.
<!-- theme: success -->
>**IH Balance: 25**

<!-- theme: warning -->
>**CB Virtual Account Balance: 15.00**

##### Request:
```json
{
  "merchant_id": "520000000321",
  "currency": "USD",
  "funding": [
    {
      "account_type": "REVENUE",
      "amount": "25.00",
      "type": "CREDIT"
    }
  ],
  "chargeback": [
    {
      "account_type": "CHARGEBACK",
      "amount": "15.00",
      "type": "CREDIT"
    }
  ]
}

```

### Using the Fee Account

If managing the Chargeback balances outside the system, additional amounts to recoup the chargeback can be added to the Fees being taken. Adding to your Gross billing would look like the below :

<!-- theme: success -->
>**IH Balance: 25**

<!-- theme: warning -->
>**Assuming a Fee of 0.32 taken, 15 Chargeback recouped**

##### Request:
```json
{
  "merchant_id": "520000000321",
  "currency": "USD",
  "funding": [
    {
      "account_type": "REVENUE",
      "amount": "25.00",
      "type": "CREDIT"
    }
  ],
  "billing": [
    {
      "account_type": "GROSS_FEE",
      "amount": "15.32",
      "type": "CREDIT"
    }
  ]
}

```
##  Reserve Management

If a submerchant is enabled for reserves through config on Exchange, instructions can be used collect and release API used to release. 

### Collecting Reserves

Reserve amounts can be sent in the `/funding/instruction` API by using the `account_type:` `RESERVE`. The amount specified will be moved to the Reserve virtual account. The `/account/balance` API can be called to check the current balance of the Reserve account for the submerchant

### Releasing and Deducting Reserves

<!-- theme: info -->
>**POST** `/reserve/release`

Reserve amounts can be released back to the submerchant, or deducted to the Aggregator. First, the `/account/balance` API should be called to check the current balance of the Reserve account.
Then, the `/reserve/release` Endpoint can be used. Specifying an `account_type:` of `RESERVE_RELEASE` will make the instruction release amounts to credit the submerchant, and an `account_type:` of `RESERVE_DEDUCTION` will deduct from the reserve to credit the Aggregator.
The `release_reason` must be specified when adjusting amounts in the reserve account. 
Amounts can be partially released, but cannot be greater than the current balance in the reserve account.
Any amounts released will move to the `RESERVE_RELEASE_ACCOUNT` , and amounts deducted will move to the `RESERVE_DEDUCTION_ACCOUNT`.
Please see full spec on the API Explorer [Here](../api/?type=post&path=/reserve/release) 

## Reimbursing the Submerchant

There may be cases where the submerchant is owed money, but the instructional hold does not have the balance to cover this. In these cases, a debit to the operating account must be made to balance the instruction. 

## Reimbursing the Aggregator

Similar to the above, there may be cases where the submerchant owes money, but the instructional hold does not have the balance to cover this. In these cases, a debit to the submerchant must be made to balance the instruction. 

## Splitting to third parties through Net Funding

For information on Splitting funds, please see the following page [here](?path=docs/getting-started/getting-started-instfunding-split.md)

