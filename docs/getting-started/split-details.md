# Split Funding by Transaction

## Instructional Split by Transaction & Managed Split by Transaction

Managed and Instructional Split by transaction both support split details sent by API for a processing MID. This will require identifiers for the transaction to be sent, along with the details on how the transaction will be split between the processing and non processing entities. Split **cannot** be defined other processing merchants on the system (only for itself).

This is accompanied by the `/split/status/` endpoint in order to check the funding status of a MIDs transaction and for its involved entities
