# Transactions

## Viewing transaction details

Exchange is able to retrieve the details of transactions that are recieved for MIDs on the system
This is facilitated by `/transaction/...` endpoints that can be viewed in the [API explorer](../api?type=post&path=/v1/apis). 
A 'query' can be created by adjusting the database operator and values being searched for:
```
{
    "location_id": {
        "operator": "EQ",
        "value": "202207180001"
    },
    "date_added": {
        "operator": "EQ",
        "value": "2022-05-16"
    }
}
```
Where available database operators for `operator` are listed below:

- EQ = Equals
- LK = Like 
- GT = Greater Than 
- LT = Lower Than 
- GE = Greater Or Equal
- LE = Lower Or Equal
- BW = Between
- LK = Like
