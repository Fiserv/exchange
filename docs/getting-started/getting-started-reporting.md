---
tags: [Getting Started, Reporting, Settlement]
---

# Reporting in Exchange

Exchange uses a set of virtual accounts and automatic settlement generation for reporting purposes. The virtual accounts provide reporting at a Summary level for money movement through the system MID-by-MID. This is represented through a set of Trade accounts, and Virtual accounts.

## Virtual Accounts

Virtual accounts hold calculated funding information for sub-merchants in order for the PayFacs to facilitate the distribution  of funds. These accounts are not representative of any physical bank accounts for the sub-merchants or PayFacs

### Trade accounts

<!-- theme: info -->
>**POST** `/account/trade-info`

The `/account/trade-info` endpoint allows the PayFac to retrieve a transaction summary of the merchant MID on a specific date. This is segregated by trade accounts, which return the following categorised 'accounts' : 

| Category                   | Key                         | Description                                                                                                              |
|----------------------------|-----------------------------|--------------------------------------------------------------------------------------------------------------------------|
| Gross Transaction Amount   | transaction_amount          | The gross amount of transactions received today.                                                                         |
| Refund Amount              | refund_amount               | The transactional amount of refunds that have been loaded in today.                                                      |
| Rejected Amount            | rejected_amount             | The amount of rejected transactions that have been loaded in today.                                                      |
| Deposit Adjustment Amount  | deposit_adjustment_amount   | The transactional amount of Deposit Adjustments that have been loaded in today. Typically, these match a Rejected transaction |
| Net Transaction Amount     | net_transaction_amount      | The Net amount of transactions for the submerchant today. This amount will be moved into the instructional hold (for instructional funding clients). net_transaction_amount = transaction_amount - refund_amount + rejected_amount - deposit_adjustment_amount. |
| Chargeback Amount          | chargeback_amount           | Reported chargeback amounts that we have loaded in today. Typically matches a Chargeback Adjustment.                      |
| Chargeback Reversal Amount | chargeback_reversal_amount  | Reported chargeback Adjustment amounts that we have loaded in today. This amount reflects actual financial movement that has occurred. Does not affect net transaction amount or instructional hold balance. |

### Instructional hold account

After the end of the transaction processing done by Exchange, the instructional hold account will be populated by the net_transaction_amount.
The PayFac will then be able to send instructions against the balance of this account during the instructional funding window. If no instruction is recieved for the day, the balance will accumulate until a new funding instruction is recieved. 
The balance in the instructional hold account is the maximum amount of avaliable funding that the `/funding/instruction` endpoint can instruct to distribute.

### Account balances

<!-- theme: info -->
>**POST** `/account/balance`

<!-- theme: info -->
>**POST** `/account/account-summary`

The `/account/balance` and `/account/account-summary` endpoints can be used to retrieve the currents balances of any virtual account. 
`/account/balance` can be used to retrieve a specific balance of an accuont at this point in time , and `/account/account-summary` retrieves a summary of  accounts on a given date.
Below is a list of virtual accounts that can be called: 

| Category                    | Key                       | Description |
|-----------------------------|---------------------------|-------------|
| Instructional Hold Account  | INSTRUCTIONAL_HOLD_ACCOUNT | Account that represents funds available for the submerchant to be instructed. Negative amounts left after the instructional hold window closes will debit the responsible party (depends on config). Should be called before creating instructions. |
| Chargeback Account          | CHARGEBACK_ACCOUNT        | Account for tracking chargebacks loaded into the system. Will accrue when chargebacks are received, or deduct when a reversal is received. Used to validate Chargeback Instructions. |
| Chargeback Recovery Account | CHARGEBACK_RECOVERY_ACCOUNT | Reports funds moving through the system for Chargeback Recoupal or reimbursement. Will show when instructions sent using the Chargeback account. A positive amount gives to the Aggregator (to cover a chargeback), and a negative amount is returning to the submerchant (chargeback reversal). |
| Merchant Fee Account        | MERCHANT_FEE_ACCOUNT      | Reports fees collected via pricing transaction billing or instructional funding will be reported here and roll up to the Fee account. Typically used in multiple outlet scenarios, where the funding level is above the outlets (Subgroup or Merchant). |
| Service Fee Account         | SERVICE_FEE_ACCOUNT       | Reports 'service' items that are billed through pricing. This includes Monthly Charges, One-off charges, Billing Instruction Charges, SaaS Charges that are done via pricing. Typically used for Auto Funding. |
| Gross Fee Account           | GROSS_FEE_ACCOUNT         | Reports fees when the submerchant is set up for gross billing. Will also report any additional GROSS_FEE instructions. |
| Fee Collect Account         | FEE_COLLECT_ACCOUNT       | Reports Gross Fees that are billed through Pricing or instructions (where instructions are type GROSS_FEE and SERVICE_FEE) that debit the merchant. Will include amounts from Service Fee (if not set up with NET) and Gross Fee if used. |
| Fee Account                 | FEE_ACCOUNT               | Represents the final Fee to be settled to the Aggregator from this submerchant. |
| Revenue Account             | REVENUE_ACCOUNT           | The final Revenue amount to be settled to the submerchant. |
| Delay Funding Account       | DELAY_FUNDING_ACCOUNT     | Reports any funds that are currently delayed, to be settled. The delay will depend on the config set for Auto Funding. |
| Rolling Reserve Account     | ROLLING_RESERVE_ACCOUNT   | Account used for Auto funding when a rolling reserve is configured. Shows the current balance for the rolling reserve (collection is based on config). |
| Reserve Account             | RESERVE_ACCOUNT           | Current Reserve balance for the submerchant  (collection done via instructions). |
| Reserve Deduction Account   | RESERVE_DEDUCTION_ACCOUNT | Reports the deductions made from the reserve (or rolling reserve), crediting the Aggregator. Release done via API or Portal. |
| Reserve Release Account     | RESERVE_RELEASE_ACCOUNT   | Reports funds released from the reserve (or rolling reserve), crediting the submerchant. Release done via API or portal. |
| Split Account               | SPLIT_ACCOUNT             | Account on Third Parties on the system used to report funds that have been split out from a submerchant on the system to a third party. Submerchants do not have this account. Will report at a summary level for amounts that are received. |
| Adjustment Account          | ADJUSTMENT_ACCOUNT        | Account used to report adjustments made in the system, typically through the adjustment block in the instructional funding API. |
| Hold Account                | HOLD_ACCOUNT              | Reports amounts that are received for a Held account when a submerchant is held. If a submerchant is unheld, any amount stored as a result of holding the submerchant is released. The Hold account will also store amounts from transaction monitoring where this results in the transaction being held, or when using transaction instructions that have not matched any transaction details. |
| Suspend Account             | SUSPEND_ACCOUNT           | Reports amounts that are received for a suspended account when a submerchant is suspended. |
| PFAC Revenue Account        | PFAC_REVENUE_ACCOUNT      | Reports on the Aggregator level the rolled-up amount of Revenue of submerchants received. |
| PFAC Reserve Account        | PFAC_RESERVE_ACCOUNT      | Reports on the Aggregator level the Reserve amounts held for submerchants. |
| PFAC Adjustment Account     | PFAC_ADJUSTMENT_ACCOUNT   | Account used to report adjustments made in the system, at the Aggregator level. |
| Settlement Reject Account   | SETTLEMENT_REJECT_ACCOUNT | Reports any ACH Rejects that come in for the submerchant. Positive amounts represent credit ACH Rejects, and negative amounts represent Debit rejects. |
| Reject Hold Account         | REJECT_HOLD_ACCOUNT       | Will report the current amount held for ACH Credit Rejects. |
| Reject Adjustment Account   | REJECT_ADJUSTMENT_ACCOUNT | Will report any amount that is adjusted from the Aggregator for an ACH Debit Reject. |
| Reject Reprocess Account    | REJECT_REPROCESS_ACCOUNT  | Reports amounts that are being reprocessed for the submerchant through the system. Reprocessed amounts will affect the final settlement for the submerchant. |



## Auto Funding Calculations

With Auto funding, Exchange is perforing calculations on the system based on configured charges that are setup. The API can be used in order to retrieve what charges were applied, and how these were broken down on a submerchant + tranasction level.

### Submerchant level transaction calculations

<!-- theme: info -->
>**POST** `/trade/details`

Using the `/trade/details` endpoint, Exchange will retrieve the summary of all processing charges applied through Auto Funding for a submerchant on the specified day. This includes a breakdown of the each charge, how much was configured for the submerchant, and how much was applied to give total insight into how this value was calculated as a whole. This is provided in an array that will display all transaction related charges.

#### Response snippet: 

```json
      "fee_details": [
        {
          "fee_amount": "10.38",
          "charge_item_external_id": "CHIBC-2DLPO-01B99-2DLPO-2DLPO-01B99-A3LK4",
          "charge_item_name": "Sample Blended Rate",
          "item_charge_breakdown": [
            {
              "fee_group": "1",
              "fee_type": "1",
              "unit_charge": "2.4500",
              "unit_amount": "125.0000",
              "unit_count": "3",
              "fee_amount": "3.0625"
            }
          ]
        }
      ]
```

| Field Name   | Type   | Example  | Description                                                                                                        |
|--------------|--------|----------|--------------------------------------------------------------------------------------------------------------------|
| fee_group    | string | 1        | Identifies the group of the charge. Currently only supports value 1                                                |
| fee_type     | string | 1        | Base or percentage charge, 1 - Percentage, 2 - Base                                                                |
| unit_charge  | string | 2.4500   | Charge that was set on boarding                                                                                    |
| unit_amount  | string | 125.0000 | The total for transactions calculated against.                                                                     |
| unit_count   | string | 3        | The amount of transactions calculated against                                                                      |
| fee_amount   | string | 3.0625   | The final amount of fee calculated for this charge items object (i.e., base fee or percentage fee calculated for). |
        
For full spec, please find API [Here](../api/?type=post&path=/account/trade-detail)

### Service fee calculations

<!-- theme: info -->
>**POST** `/billing/fee-details`

Within Auto funding, 'service billing' can be added to a submerchant. This allows for the user to bill for non-transaction related charges such as a monthly charge. By calling the `/billing/fee-details` endpoint this will retrieve any service charge items that have been billed for that day. 

```json
{
  "result": "SUCCESS",
  "billing_merchant_id": "520000004321",
  "total_amount": "5.1500",
  "fee_details": [
    {
      "merchant_id": "520000004321",
      "billing_type": "ACQUIRING_CHARGE",
      "charge_item_external_id": "CHIBC-2DLPO-01B99-2DLPO-2DLPO-01B99-A3LK4",
      "charge_title": "Monthly Fee",
      "date": "2022-01-31",
      "unit_charge": "5.1500",
      "quantity": "1",
      "amount": "5.1500"
    }
  ]
}
```
| Field Name               | Type   | Example                                | Description                                          |
|--------------------------|--------|----------------------------------------|------------------------------------------------------|
| merchant_id              | string | 520000004321                           | The submerchant MID that charge has been applied to. |
| billing_type             | string | ACQUIRING_CHARGE                       | Defines what type of charge is applied. Enum: ACQUIRING_CHARGE, EQUIPMENT, EQUIPMENT_SERVICE. |
| charge_item_external_id  | string | CHIBC-2DLPO-01B99-2DLPO-2DLPO-01B99-A3LK4 | External ID of the charge being applied.            |
| charge_title             | string | Sample Blended Rate                   | Configured title of the charge applied.              |
| date                     | string | 2022-01-01                            | Date the charge was applied.                         |
| unit_charge              | string | 0.5000                                | Amount configured to bill from the charge added at the submerchant. |
| quantity                 | string | 1                                     | Quantity of billing applied from charge.             |
| amount                   | string | 0.5000                                | Billing calculated.                                  |

## Settlement API

Settlements can be retrieved by UI or API and will show the type of settlement (Credit or Debit), effective date, settlement details, status and reference. We will only show settlements if Exchange is handling funding or billing for the submerchant.

### Submerchant Settlements

<!-- theme: info -->
>**POST** `/account/settlement-info

This is handled using the `/account/settlement-info` endpoint on a MID-by-MID basis. 
The reference is uniquely assigned when the settlement is generated, and the *effective date* is the date that this settlement will actually be funded to the merchants bank account.

### Settlement Rejects (ACH rejects)

<!-- theme: info -->
>**POST** `/settlement/rejects`

In the scenario that an ACH reject occurs, the `/settlement/rejects` will report a rejected settlement for the MID.
The settlement reference can be used to trade a rejected settlement to its inital settlement response from `/account/settlement-info` in order to see the instructions that were sent.
The reject endpoint will pull details for the rejected settlement, including a reason code, and the deposit that was rejected for the sub-merchant. 

### Aggregator Settlements

Aggregator Settlements are rolled into one ACH settlement each day. 

For full spec, please find API [Here](../api?type=post&path=/account/billing/fee-details) 

