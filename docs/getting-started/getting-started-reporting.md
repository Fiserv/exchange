---
tags: [Getting Started, Reporting]
---

# Reporting in Exchange

Exchange uses a set of virtual accounts and automatic settlement generation for reporting purposes. 

# Summary level reporting accounts

At a summary level, we also report money movement through the system MID-by-MID

## Virtual Accounts

Virtual accounts hold calculated funding information for sub-merchants in order for the PayFacs to facilitate the distribution  of funds. These accounts are not representative of any phyisical bank accounts for the sub-merchants or PayFacs

### Trade accounts

<!-- theme: info -->
>**POST** `/account/trade-info`

The `/account/trade-info` endpoint allows the PayFac to retrieve a transaction summary of the merchant MID on a specific date. This is segregated by trade accounts, which return the following categorised 'accounts' : 

| Category      | Key |
| :---:        |    :----:   |
| Gross Transaction Amount      | transaction_amount       |
| Refund Amount   | refund_amount        |
| Deposit Adjustment Amount      | deposit_adjustment_amount       |
| Net Transaction Amount   | net_transaction_amount        |
| Chargeback Amount      | chargeback_amount       |
| Chargeback Reversal Amount   | chargeback_reversal_amount        |

### Instructional hold account

After the end of the transaction processing done by Exchange, the instructional hold account will be populated by the net_transaction_amount.
The PayFac will then be able to send instructions against the balance of this account during the instructional funding window. If no instruction is recieved for the day, the balance will accumulate until a new funding instruction is recieved. 
The balance in the instructional hold account is the maximum amount of avaliable funding that the `/funding/instruction` endpoint can instruct to distribute.

### Account balances

<!-- theme: info -->
>**POST** `/account/balance`

The `/account/balance` endpoint can be used to retrieve the balance of any virtual account: 
- REVENUE_ACCOUNT
- FEE_ACCOUNT
- SERVICE_FEE_ACCOUNT
- RESERVE_ACCOUNT
- CHARGEBACK_ACCOUNT

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

