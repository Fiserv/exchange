# Transactions

## Viewing transaction details

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
