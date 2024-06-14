# Net Instructional Funding Funding

This section will focus on creating Funding instructions for NET scenarios. Please refer to the main [Funding](?path=docs/getting-started/getting-started-funding.md) page first for details on the Accounts and Process flow.

## What is Net Instructional funding?

For NET instructions, we always try to net out any billing before generating settlement, so that either 1 Credit is generated or 1 Debit is generated for the submerchant. This is primarily done by utilising the `FUNDING` block on the `/funding/instruction` endpoint.

Instructional Split funding extends the functionality of the `/funding/instruction` in order to allow a 'split_details' block, where the split is defined at a summary level for the processing MID, and 'non-processing' entities defined. Fees taken from the split amount will be received by the non-processing PayFac.

## Constructing a NET instruction 

The funding block is used to instruct amounts where the source of the instruction is the instructional hold.
In the below example for Net funding, we include the Revenue, Chargeback, and Fee in the funding block to achieve a NET scenario.
Chargeback Validation will check that the chargeback account can support this amount being taken.

The account types affect what action is taken on the account.
For the funding block:
<ul>
  <li> type: CREDIT - Credits the specified account from the available instructional hold balance./li>
  <li> type: DEBIT - Credits the instructional hold balance from the specified account. This cannot be used to bring the instructional hold to a balance greater than it was before unless it is negative.</li>
</ul>

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

## Managing Chargeback through NET instructions

Chargeback is represented through virtual accounts on the system, which means there are a few options on recouping or reimbursing amounts for the chargeback through instructional funding.

The Chargeback virtual account keeps balances from Chargeback Adjustments that happen outside the system. This represents information that the chargeback has occured, and this balance is used for validation when instruction funds with an `"account_type": "CHARGEBACK"` 

### Using the Chargeback account

In order to use the chargeback account in the instruction, the `"account_type": "CHARGEBACK"` must be specified. This will make the instruction validate against the current Chargeback Virtual Account Balance.
<!-- theme: success -->
>**IH Balance: 25**

<!-- theme: warning -->
>**CB Virtual Account Balance: 5.00**
##### Request:
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

### Rolling this up into the Fee amount

If managing the Chargeback balances outside the system, additional amounts to recoup the chargeback can be added to the Fee amount. This can be added as a NET fee, or debited directly as a seperate Gross Fee. Adding to your NET funding would look like the below :

<!-- theme: success -->
>**IH Balance: 25**

<!-- theme: warning -->
>**Standard Fee of 0.32 taken**
##### Request:
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
      "account_type": "FEE",
      "amount": "5.32",
      "type": "CREDIT"
    }
  ]
}
```

## Reimbursing the Submerchant

There may be cases where the submerchant is owed money, but the instructional hold does not have the balance to cover this. In these cases, a debit to the operating account must be made to balance the instruction. 


