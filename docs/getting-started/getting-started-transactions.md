---
tags: [Getting Started, Reporting, Transactions, Chargebacks, Auto funding]
---

# Transactions in Exchange

Exchange consumes transactions into the system daily, making these available in our reporting APIs where these flow into the [virtual accounts](../docs/getting-started/getting-started-reporting.md). 
These can be found on the set of `/transaction/...` endpoints that can be viewied on the [API Explorer](../api/?type=post&path-/transaction)

## Transaction requests

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

## Auto-funding calculations

### Processing fee caluclations

To retrieve calculations performed by Auto fundings processing charges at a tranasction level, the `fee_details` block in the `/transaction` , `/transaction/chargeback-adjustments`, `/transaction/rejects`  endpoints can be used. This provides a breakdown of all charge items that have applied for this charge, and how they were calculated. For full spec, please find API [Here](../api/?type=post&path=/transaction)
### Service fee calculations

Within Auto funding, 'service billing' can be added to a submerchant. This allows for the user to bill for non-transaction related charges such as a monthly charge. By calling the `/billing/fee-details` endpoint this will retrieve any service charge items that have been billed for that day. For full spec, please find API [Here](../api?type=post&path=/account/billing/fee-details) 

