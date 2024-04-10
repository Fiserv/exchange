# Reporting in Exchange

Exchange functions using virtual accounts and automatic settlement generation for reporting purposes. 

## Settlement

Settlements can be retrieved by UI or API and will show the type of settlement (Credit or Debit), effective date, settlement details, status and reference. 
This is handled using the `/account/settlement-info` endpoint on a MID basis. 
The reference is uniquely assigned when the settlement is generated, and the *effective date* is the date that this settlement will actually be funded to the merchants bank account.

## Rejects

In the scenario that an ACH reject occurs, the `/settlement/rejects` will report a rejected settlement for the MID.
The settlement reference can be used to trade a rejected settlement to its inital settlement response from `/account/settlement-info` in order to see the instructions that were sent.
The reject endpoint will pull details for the rejected settlement, including a reason code, and the deposit that was rejected for the sub-merchant. 

## Transaction details

Exchange is able to retrieve the details of transactions that are recieved for MIDs on the system
This is facilitated by `/transaction/...` endpoints that can be viewed in the API Explorer. 
A 'query' can be created by adjusting the database operator and values being searched for:
```
        "location_id": {
            "operator": "EQ",
            "value": "202205290001"
            },
        "date_added": {
            "operator": "EQ",
            "value": "2022-05-16"
        }
```

## Virtual accounts

Virtual accounts hold calculated funding information for sub-merchants in order for the PayFacs to facilitate the distribution  of funds. These accounts are not representative of any phyisical bank accounts for the sub-merchants or PayFacs

### Trade accounts

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

The `/account/balance` endpoint can be used to retrieve the balance of any virtual account: 
- REVENUE_ACCOUNT
- FEE_ACCOUNT
- SERVICE_FEE_ACCOUNT
- RESERVE_ACCOUNT
- CHARGEBACK_ACCOUNT

## Auto Funding Calculations

With Auto funding, Exchange is perforing calculations on the system based on configured charges that are setup. The API can be used in order to retrieve what charges were applied, and how these were broken down on a submerchant + tranasction level.

### Submerchant level calculations

Using the `/trade/details` endpoint, Exchange will retrieve the summary of all processing charges applied through Auto Funding for a submerchant on the specified day. This includes a breakdown of the each charge, how much was configured for the submerchant, and how much was applied to give total insight into how this value was calculated as a whole. For full spec, please find API [Here]{https://developer.fiserv.com/product/Exchange/api/?type=post&path=/account/trade-details&branch=main&version=3.0.0}

### Service fee calculations

Within Auto funding, 'service billing' can be added to a submerchant. This allows for the user to bill for non-transaction related charges such as a monthly charge. By calling the `/billing/fee-details` endpointm this will retrieve any service charge items that have been billed for that day. For full spec, please find API [Here]{https://developer.fiserv.com/product/Exchange/api/?type=post&path=/account/billing/fee-details&branch=main&version=3.0.0} 

### Transaction level calculations

To retrieve calculations performed by Auto fundings processing charges at a tranasction level, the `fee_details` block in the `/transaction` , `/transaction/chargeback-adjustments`, `/transaction/rejects`  endpoints can be used. This provides a breakdown of all charge items that have applied for this charge, and how they were calculated. For full spec, please find API [Here]{https://developer.fiserv.com/product/Exchange/api/?type=post&path=/transaction&branch=main&version=3.0.0}
