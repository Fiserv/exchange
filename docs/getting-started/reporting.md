# Reporting in Exchange

Exchange functions uses virtual accounts and automatic settlement generation for reporting purposes. 

## Settlement

Settlements can be retrieved by UI or API and will show the type of settlement (Credit or Debit), effective date, settlement details, status and reference. 
This is handled using the `/account/settlement-info` endpoint on a MID basis. This reports the 
The reference is uniquely assigned when the settlement is generated, and the *effective date* is the date that this settlement will actually be funded to the Merchant Bank account.

## Rejects

In the scenario that an ACH reject occurs, the `/settlement/rejects` will report a rejected settlement for the MID.

## Transaction Details

Exchange is able to retrieve the details of transactions that are recieved for MIDs on the system

## Virtual Accounts
### Trade Accounts

### Account Balances
