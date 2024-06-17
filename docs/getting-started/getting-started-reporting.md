---
tags: [Getting Started, Reporting]
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

The `/account/balance` endpoint can be used to retrieve the balance of any virtual account: 

| Category                      | Key                         | Description                                                                      |
|-------------------------------|-----------------------------|----------------------------------------------------------------------------------|
| TRADE ACCOUNT                 | TRADE_ACCOUNT               | Account used for trade settlements and transactions.                             |
| CHARGEBACK ACCOUNT            | CHARGEBACK_ACCOUNT          | Account for tracking chargebacks received from customers.                        |
| FEE ACCOUNT                   | FEE_ACCOUNT                 | Account designated for the accumulation of fees charged.                         |
| REVENUE ACCOUNT               | REVENUE_ACCOUNT             | Account where net revenue is recorded and tracked.                               |
| RESERVE ACCOUNT               | RESERVE_ACCOUNT             | Account holding funds in reserve for contingencies.                              |
| CHARGEBACK RECOVERY ACCOUNT   | CHARGEBACK_RECOVERY_ACCOUNT | Account for funds recovered from chargebacks.                                    |
| INSTRUCTIONAL HOLD ACCOUNT    | INSTRUCTIONAL_HOLD_ACCOUNT  | Account holding funds temporarily as per specific instructions.                  |
| ROLLING RESERVE ACCOUNT       | ROLLING_RESERVE_ACCOUNT     | Account that holds a rolling reserve for risk management.                        |
| RESERVE DEDUCTION ACCOUNT     | RESERVE_DEDUCTION_ACCOUNT   | Account for deductions made from the reserve.                                    |
| RESERVE RELEASE ACCOUNT       | RESERVE_RELEASE_ACCOUNT     | Account for releasing funds previously held in reserve.                          |
| MERCHANT FEE ACCOUNT          | MERCHANT_FEE_ACCOUNT        | Account where merchant-related fees are collected.                               |
| SERVICE FEE ACCOUNT           | SERVICE_FEE_ACCOUNT         | Account for service-related fees charged.                                        |
| FEE COLLECT ACCOUNT           | FEE_COLLECT_ACCOUNT         | Account used to collect various types of fees.                                   |
| REJECT HOLD ACCOUNT           | REJECT_HOLD_ACCOUNT         | Account used to hold funds related to rejected transactions.                     |
| ADJUSTMENT ACCOUNT            | ADJUSTMENT_ACCOUNT          | Account for recording financial adjustments.                                     |
| REJECT REPROCESS ACCOUNT      | REJECT_REPROCESS_ACCOUNT    | Account dedicated to reprocessing rejected transactions.                         |
| SUSPEND ACCOUNT               | SUSPEND_ACCOUNT             | Account that holds suspended funds until a decision is made.                     |
| HOLD ACCOUNT                  | HOLD_ACCOUNT                | General account used for holding funds temporarily.                              |
| PFAC REVENUE ACCOUNT          | PFAC_REVENUE_ACCOUNT        | Account for Payment Facilitator's net revenue tracking.                          |
| PFAC RESERVE ACCOUNT          | PFAC_RESERVE_ACCOUNT        | Reserve account specifically for a Payment Facilitator.                          |
| DELAY FUNDING ACCOUNT         | DELAY_FUNDING_ACCOUNT       | Account used to delay funding for transactions, often for review.                |
| GROSS FEE ACCOUNT             | GROSS_FEE_ACCOUNT           | Account for the total gross fees before any deductions or adjustments.           |
| REJECT ADJUSTMENT ACCOUNT     | REJECT_ADJUSTMENT_ACCOUNT   | Account used for adjustments relating to rejected transactions.                  |
| PFAC ADJUSTMENT ACCOUNT       | PFAC_ADJUSTMENT_ACCOUNT     | Account for financial adjustments specific to a Payment Facilitator.             |
| SPLIT ACCOUNT                 | SPLIT_ACCOUNT               | Account utilized when splitting funds between different parties.                 |

## Auto Funding Calculations

With Auto funding, Exchange is perforing calculations on the system based on configured charges that are setup. The API can be used in order to retrieve what charges were applied, and how these were broken down on a submerchant + tranasction level.

### Submerchant level transaction calculations

<!-- theme: info -->
>**POST** `/trade/details`

Using the `/trade/details` endpoint, Exchange will retrieve the summary of all processing charges applied through Auto Funding for a submerchant on the specified day. This includes a breakdown of the each charge, how much was configured for the submerchant, and how much was applied to give total insight into how this value was calculated as a whole. For full spec, please find API [Here](../api/?type=post&path=/account/trade-detail)

### Service fee calculations

<!-- theme: info -->
>**POST** `/billing/fee-details`

Within Auto funding, 'service billing' can be added to a submerchant. This allows for the user to bill for non-transaction related charges such as a monthly charge. By calling the `/billing/fee-details` endpoint this will retrieve any service charge items that have been billed for that day. For full spec, please find API [Here](../api?type=post&path=/account/billing/fee-details) 

