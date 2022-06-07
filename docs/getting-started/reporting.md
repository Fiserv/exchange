# Reporting in Exchange

Exchange functions uses virtual accounts and automatic settlement generation for reporting purposes. 

## Settlement

Settlements can be retrieved by UI or API and will show the type of settlement (Credit or Debit), effective date, settlement details, status and reference. 
This is handled using the `/account/settlement-info` endpoint on a MID basis. This reports the 
The reference is uniquely assigned when the settlement is generated, and the *effective date* is the date that this settlement will actually be funded to the Merchant Bank account.

## Rejects

In the scenario that an ACH reject occurs, the `/settlement/rejects` will report a rejected settlement for the MID.
The settlement reference can be used to trade a rejected settlement to its inital settlement response from `/account/settlement-info` in order to see the instructions that were sent.
The reject endpoint will pull details for the rejected settlement, including a reason code, and the deposit that was rejected for the merchant. The Fee amount taken for the PayFac is removed from the response for a merchant rejected settlement. 

## Transaction Details

Exchange is able to retrieve the details of transactions that are recieved for MIDs on the system

## Virtual Accounts
### Trade Accounts

### Account Balances
