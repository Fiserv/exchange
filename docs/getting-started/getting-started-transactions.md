---
tags: [Getting Started, Reporting, Transactions, Chargebacks, Auto funding]
---

# Transactions in Exchange

Exchange consumes transactions into the system daily, making these available in our reporting APIs where these flow into the [virtual accounts](../docs/getting-started/getting-started-reporting.md) if funding is being done through Exchange. 
These can be called on the set of `/transaction/...` endpoints that can be viewied on the [API Explorer](../api/?type=post&path-/transaction). The Field `date_added` indicates the date this was added into our system.

## Requests

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
This can be used with other operators and values that can be seen on the [API Explorer](../api/?type=post&path-/transaction)

## Transactions

<!-- theme: info -->
>**POST** `/transaction`

Transactions include sales and refunds that are captured. 

## Rejects

<!-- theme: info -->
>**POST** `/transaction/rejects`

Rejected tranasctions are seperated into the rejects endpoint


## Chargeback Adjustments

<!-- theme: info -->
>**POST** `/transaction/chargeback-adjustments`

Chargeback Adjustments report actual financial adjustments that have been made relating to a chargeback. Can be used in a fund-the-pfac setup to know when a chargeback needs to be recouped or reimbursed from a submerchant.  

## Chargebacks

<!-- theme: info -->
>**POST** `/transaction/chargebacks`

Reports the movement on the chargeback case itself.

## Authorizations

<!-- theme: info -->
>**POST** `/transaction/authorizations`

Reports authorizations being loaded into the system, which typically refresh every 15 minutes.

## Adjustments

<!-- theme: info -->
>**POST** `/transaction/adjustments`



## Auto-funding calculations

Auto funding on exchange performs calculations automatically based on configurations set for that submerchant. As this is being done by the system, we will add the calculations being performed onto the transactions this is added to.

### Processing fee caluclations

To retrieve calculations performed by Auto fundings processing charges at a transaction level, the `fee_details` block in the `/transaction` , `/transaction/chargeback-adjustments`, `/transaction/rejects`  endpoints can be used. This provides a breakdown of all charge items that have applied for this charge, and how they were calculated. For full spec, please find API [here](../api/?type=post&path=/transaction)
### Service fee calculations

Within Auto funding, 'service billing' can be added to a submerchant. This allows for the user to bill for non-transaction related charges such as a monthly charge. By calling the `/billing/fee-details` endpoint this will retrieve any service charge items that have been billed for that day. For full spec, please find API [here](../api?type=post&path=/account/billing/fee-details) 

