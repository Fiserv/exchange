
# Net Instructional Funding 

This section will focus on creating Funding instructions for NET scenarios. Please refer to the main [Funding](?path=docs/getting-started/getting-started-funding.md) page first for details on the Accounts and Process flow.

## What is Net Instructional funding?

Instructional funding allows instructions to be sent via API to the instructional hold, for fees to be delegated, and funds to be settled to the sub-merchant.
For NET instructions, we will always try to net out any billing before generating settlement, so that either 1 Credit is generated or 1 Debit is generated for the sub-merchant. This is primarily done by utilizing the `FUNDING` block on the `/funding/instruction` endpoint.

Instructional Split funding extends the functionality of the `/funding/instruction` in order to allow a 'split_details' block, where the split is defined at a summary level for the processing MID, and 'non-processing' entities defined. Fees taken from the split amount will be received by the non-processing PayFac.

## Constructing an instruction for Net Funding 

<!-- theme: info -->
>**POST** `/funding/instruction`

The funding block is used to instruct amounts where the source of the instruction is the instructional hold.
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
The settlement that will generate from this instruction will be a settlement of $84.50 to the sub-merchant, and $15.50 to the Aggregator 

## Chargeback Management for Net Funding

Chargeback is represented through virtual accounts on the system, which means there are a few options on recouping or reimbursing amounts for the chargeback through instructional funding.

The Chargeback virtual account keeps balances from Chargeback Adjustments that happen outside the system. This represents information that the chargeback has occurred, and this balance is used for validation when instruction funds with an `"account_type": "CHARGEBACK"`. There are two ways of doing this through Net instructions, seen below.

### Using the Chargeback Account

In order to use the chargeback account in the instruction, the `"account_type": "CHARGEBACK"` must be specified. This will make the instruction validate against the current Chargeback Virtual Account Balance.

##### Request:

<!-- theme: success -->
>**IH Balance: 25**

<!-- theme: warning -->
>**CB Virtual Account Balance: 5.00**

```json
{
  "merchant_id": "520000000321",
  "currency": "USD",
  "funding": [
    {
      "account_type": "REVENUE",
      "amount": "20.00",
      "type": "CREDIT"
    },
    {
      "account_type": "CHARGEBACK",
      "amount": "5.00",
      "type": "CREDIT"
    }
  ]
}
```

### Using the Fee Account

If managing the Chargeback balances outside the system, additional amounts to recoup the chargeback can be added to the Fee amount. This can be added as a NET fee, or debited directly as a separate Gross Fee. Adding to your NET funding would look like the below :

##### Request:

<!-- theme: success -->
>**IH Balance: 25**

<!-- theme: warning -->
>**Assuming a Fee of 0.32 taken**

```json
{
  "merchant_id": "520000000321",
  "currency": "USD",
  "funding": [
    {
      "account_type": "REVENUE",
      "amount": "19.68",
      "type": "CREDIT"
    },
    {
      "account_type": "FEE",
      "amount": "5.32",
      "type": "CREDIT"
    }
  ]
}
```

##  Reserve Management

If a sub-merchant is enabled for reserves through config on Exchange, instructions can be used collect and release API used to release. 

### Collecting Reserves

Reserve amounts can be sent in the `/funding/instruction` API by using the `account_type:` `RESERVE`. The amount specified will be moved to the Reserve virtual account. The `/account/balance` API can be called to check the current balance of the Reserve account for the sub-merchant

### Releasing and Deducting Reserves

<!-- theme: info -->
>**POST** `/reserve/release`

Reserve amounts can be released back to the sub-merchant or deducted from the sub-merchant and credited to the Aggregator. First, the `/account/balance` API should be called to check the current balance of the Reserve account.
Then, the `/reserve/release` Endpoint can be used. Specifying an `account_type:` of `RESERVE_RELEASE` will make the instruction release amounts to credit the sub-merchant, and an `account_type:` of `RESERVE_DEDUCTION` will deduct from the reserve to credit the Aggregator.
The `release_reason` must be specified when adjusting amounts in the reserve account. 
Amounts can be partially released, but cannot be greater than the current balance in the reserve account.
Any amounts released will move to the `RESERVE_RELEASE_ACCOUNT` , and amounts deducted will move to the `RESERVE_DEDUCTION_ACCOUNT`.
Please see full spec on the API Explorer [Here](../api/?type=post&path=/reserve/release) 

##  Split Account

The Funding API can also handle a `split_details` object, which can be used to send amounts to third parties that are boarded on the system.
For example, if we wanted to include a split of 4.50 to a third party on the system from the sub-merchants normal revenue, we would include the split details object with a type `CREDIT`

<!-- theme: success -->
>**IH Balance: 100**

```json
{
  "merchant_id": "520000000321",
  "currency": "USD",
  "funding": [
    {
      "account_type": "REVENUE",
      "amount": "94.50",
      "type": "CREDIT",
      "split_details": [
        {
          "merchant_id": "400000000005",
          "accounts": {
            "account_type": "REVENUE",
            "amount": "4.50",
            "type": "CREDIT"
          }
        }
      ]
    }
    {
      "account_type": "FEE",
      "amount": "5.50",
      "type": "CREDIT"
    }
  ]
}
```

## Additional Scenarios

Some scenarios may require additional debits or credits to keep the instruction balanced. Please see some additional scenarios below

#### Reimbursing the Sub-Merchant

There may be cases where the sub-merchant is owed money, but the instructional hold does not have the balance to cover this. In these cases, a debit to the operating account must be made to balance the instruction. 

#### Reimbursing the Aggregator

Similar to the above, there may be cases where the sub-merchant owes money, but the instructional hold does not have the balance to cover this. In these cases, a debit to the sub-merchant must be made to balance the instruction. 

#### Splitting to third parties through Net Funding

For information on Splitting funds, please see the following page [here](?path=docs/getting-started/getting-started-instfunding-split.md)


