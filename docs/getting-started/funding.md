# Funding
For solutions that are instruction driven, Exchange offers funding API to facilitate the funding. 
# Instructional Funding

For Instructional Funding, the `/funding/instruction/` endpoint can be uesd in order to direct funds for a given merchant ID. 
Instructional funding also supports instructions sent through the `/funding/detailed-instruction/` endpoint, where additional information can be added within an instruction through a 'details' block for reporting purposes. (details do not affect the funding, just act as information)

# Split Funding
## Instructional Split

Instructional Split funding extends the functionality of the `/funding/instruction/` in order to facilitate the 'SPLIT' block, where the split is defined at a summary level for the processing MID, and 'non-processing' entities defined. Fees taken from the split amount will be recieved by the non-processing PayFac.
