---
tags: [Getting Started, Funding, Settlement]
---

# Settlements in Exchange

Settlements can be retrieved by UI or API and will show the type of settlement (Credit or Debit), effective date, settlement details, status and reference. 

## Submerchant Settlements

This is handled using the `/account/settlement-info` endpoint on a MID basis. 
The reference is uniquely assigned when the settlement is generated, and the *effective date* is the date that this settlement will actually be funded to the merchants bank account.

## PayFac Settlements

PayFac Settlements are rolled into one ACH settlement each day. 

## Settlement Rejects (ACH rejects)
In the scenario that an ACH reject occurs, the `/settlement/rejects` will report a rejected settlement for the MID.
The settlement reference can be used to trade a rejected settlement to its inital settlement response from `/account/settlement-info` in order to see the instructions that were sent.
The reject endpoint will pull details for the rejected settlement, including a reason code, and the deposit that was rejected for the sub-merchant. 
