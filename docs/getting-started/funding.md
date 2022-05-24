# Funding
For solutions that are instruction driven, Exchange offers funding API to facilitate the funding. 
# Instructionl Funding

For Instructional Funding, the `/funding/instruction/` endpoint can be uesd in order to direct funds for a given merchant ID. 
Instructional funding also supports instructions sent through the `/funding/detailed-instruction/` endpoint, where additional information can be added within an instruction through a 'details' block for reporting purposes. (details do not affect the funding, just act as information)

# Split Funding
## Instructional Split

Instructional Split funding extends the functionality of the `/funding/instruction/` in rder to facilitate the 'SPLIT' block, where the split is defined at a summary level for the processing MID, and 'non-processing' entities defined. Fees taken from the split amount will be recieved by the non-processing PayFac.

## Instructional Split by Transaction & Managed Split by Transaction

Managed and Instructional Split by transaction both support split details sent by API for a processing MID. This will require identifiers for the transaction to be sent, along with the details on how the transaction will be split between the processing and non processing entities. Split **cannot** be defined other processing merchants on the system (only for itself).

This is accompanied by the `/split/status/` endpoint in order to check the funding status of a MIDs transaction and for its involed entities
