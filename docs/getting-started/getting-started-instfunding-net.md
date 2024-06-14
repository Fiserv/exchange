# Net Instructional Funding Funding

This section will focus on creating Funding instructions for NET scenarios. Please refer to the main [Funding](?path=docs/getting-started/getting-started-funding.md) page first for details on the Accounts and Process flow.

## What is Net Instructional funding?

For NET instructions, we always try to net out any billing before generating settlement, so that either 1 Credit is generated or 1 Debit is generated for the submerchant. This is primarily done by utilising the `FUNDING` block on the `/funding/instruction` endpoint.

Instructional Split funding extends the functionality of the `/funding/instruction` in order to allow a 'split_details' block, where the split is defined at a summary level for the processing MID, and 'non-processing' entities defined. Fees taken from the split amount will be received by the non-processing PayFac.

## Constructing a NET instruction 

<!--
type: tab
titles: Net funding, JSON instructional funding example
-->

The funding block is used to instruct amounts where the source of the instruction is the instructional hold.
In the below example for Net funding, we include the Revenue, Chargeback, and Fee in the funding block to achieve a NET scenario.
Chargeback Validation will check that the chargeback account can support this amount being taken.

The account types affect what action is taken on the account.
For the funding block:
<ul>
  <li> type: CREDIT - Credits the specified account from the available instructional hold balance./li>
  <li> type: DEBIT - Credits the instructional hold balance from the specified account. This cannot be used to bring the instructional hold to a balance greater than it was before unless it is negative.</li>
</ul>

<!-- theme: sucess -->
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

---

<!-- type: tab -->

JSON format for `/funding/instruction` , where `REVENUE_ACCOUNT` defines the merchant revenue received from Instructional hold and `FEE_ACCOUNT` defines the PayFac fee taken and `SPLIT_ACCOUNT` is used to define the split amounts sent to third parties. The `"split_details"` block can direct funds to multiple third parties on the system, where the mid used `merchant_id` will be the `internal_mid` of the third party on the system. 

Supported accounts added to this request include:

```json

```

<!-- type: tab-end -->

