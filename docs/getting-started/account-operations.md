#  Account Operations and Settlement Info
## Virtual Accounts  

Exchange uses 'virtual accounts' in order to segregate funding for sub-merchants on the system. These virtual accounts are present for each level of the sub-merchant hierarchy, and the PayFac hierarchy in Exchange. These do not correlate to any *actual* bank accounts for the sub-merchants or PayFac.

## Virtual Account Operations

Account Operations allow the PayFac to gather information about the virtual accounts on the system. This can be requested individually using the `/account/balance` endpoint or a summary of all accounts for a MID can be requested using `/account/account-summary` endpoint. Please see the Account operation section in the  [API explorer](../api?type=post&path=/v1/apis) for full API specs on these requests.

### Get Account Summary

The PayFac is able to retrieve a summary of accounts for a given MID using the `/account/account-summary` endpoint. 

### Get Account Balance

The `/account/balance` endpoint can be used to retrieve the balance of any virtual account: 
- REVENUE_ACCOUNT
- FEE_ACCOUNT
- SERVICE_FEE_ACCOUNT
- RESERVE_ACCOUNT
- CHARGEBACK_ACCOUNT

The request for this is constructed as such below, where the account_type is the account balance being retrieved for the MID.

```
{
    "merchant_id": "223456789064",
    "currency": "USD",
    "account_type": "INSTRUCTIONAL_HOLD_ACCOUNT"
}
```

## Trade Accounts

The trade accounts are used to retrieve and calculate the transaction summary by the system. The net transaction amount wll be the amount avaliable for instructions, as ths will populate into the virtual account 'instructional hold account' during the instructional window for the system.

The following trade accounts are used by the system:

| Category      | Key |
| :---:        |    :----:   |
| Gross Transaction Amount      | transaction_amount       |
| Refund Amount   | refund_amount        |
| Deposit Adjustment Amount      | deposit_adjustment_amount       |
| Net Transaction Amount   | net_transaction_amount        |
| Chargeback Amount      | chargeback_amount       |
| Chargeback Reversal Amount   | chargeback_reversal_amount        |

Where the `net_tranasction_amount` is calculated by:  
net_transaction_amount = transaction_amount - refund_amount + rejected_amount - deposit_adjustments_amount.

### Get Trade Info

The `/account/trade-info` endpoint allows the PayFac to retrieve a transaction summary of the sub-merchants MID on a specific date by API, and will return the amounts in each trade account listed in the above table, as well as the number of transactions received.

## Settlement info

Settlements can be retrieved by UI or API and will show the type of settlement (Credit or Debit), effective date, settlement details, status and reference. 
This is handled using the `/account/settlement-info` endpoint on a MID by MID basis.
The reference is uniquely assigned when the settlement is generated, and the *effective date* is the date that this settlement will actually be funded to the sub-merchants Bank account.

### Get settlement info

Retrieve the settlement info for a given MID on a specified date through the `/account/settlement-info` endpoint. Can be used for reconciling funding instructions and settlement output by Exchange.

### Get Settlement Rejects

In the scenario that an ACH reject occurs, the `/settlement/rejects` will report a rejected settlement for the MID.
The settlement reference can be used to trace a rejected settlement to its inital settlement response from `/account/settlement-info` in order to see the instructions that were sent. The reject endpoint will pull details for the rejected settlement, including a reason code, and the deposit that was rejected for the sub-merchants. The Fee amount taken for the PayFac is removed from the response for a sub-merchants rejected settlement. 

