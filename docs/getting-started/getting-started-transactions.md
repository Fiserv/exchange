---
tags: [Getting Started, Reporting, Transactions, Chargebacks, Auto funding]
---

# Transactions in Exchange

Exchange processes transactions daily, making them available in our reporting APIs. These transactions flow into the [virtual accounts](../docs/getting-started/getting-started-reporting.md) if funding is conducted through Exchange. You can access them via the `/transaction/...` endpoints visible on the [API Explorer](../api/?type=post&path-/transaction). The field `date_added` indicates the date the transaction was added to our system.

## Requests

A 'query' can be created by adjusting the database operator and values being searched for:
```
{
    "location_id": {
        "operator": "EQ",
        "value": "202205290001"
    },
    "date_added": {
        "operator": "EQ",
        "value": "2022-05-16"
    }
}
```
This can be extended with other operators and values viewable on the [API Explorer](../api/?type=post&path-/transaction).

## Transactions

<!-- theme: info -->
>**POST** `/transaction`

Transactions include sales and refunds that are captured.

## Rejects

<!-- theme: info -->
>**POST** `/transaction/rejects`

Rejected transactions are separated into the rejects endpoint.


## Chargeback Adjustments

<!-- theme: info -->
>**POST** `/transaction/chargeback-adjustments`

Chargeback Adjustments report actual financial adjustments related to a chargeback. This can be used in a fund-the-PFAC setup to know when a chargeback needs to be recouped or reimbursed from a sub-merchant.  

## Chargebacks

<!-- theme: info -->
>**POST** `/transaction/chargebacks`

Reports the movement on the chargeback case itself.

## Authorizations

<!-- theme: info -->
>**POST** `/transaction/authorizations`

Reports authorizations being loaded into the system, typically every 15 minutes.

## Adjustments

<!-- theme: info -->
>**POST** `/transaction/adjustments`

## Auto-funding calculations

Auto funding on Exchange performs calculations automatically based on configurations set for that sub-merchant. As this is done by the system, the calculations performed will be added to the corresponding transactions.

### Processing fee caluclations

To retrieve calculations performed by Auto fundings processing charges at a transaction level, the `fee_details` block in the `/transaction` , `/transaction/chargeback-adjustments`, `/transaction/rejects`  endpoints can be used. This provides a breakdown of all charge items that have applied for this charge, and how they were calculated. For full spec, please find API [here](../api/?type=post&path=/transaction)
### Service fee calculations

Within Auto funding, 'service billing' can be added to a submerchant. This allows for the user to bill for non-transaction related charges such as a monthly charge. By calling the `/billing/fee-details` endpoint this will retrieve any service charge items that have been billed for that day. For full spec, please find API [here](../api?type=post&path=/account/billing/fee-details) 

