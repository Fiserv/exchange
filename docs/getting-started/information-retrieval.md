# Information Retrieval

## Bank Retrieval

The Bank Details for a Merchant that is boarded on the system under the PayFac can be retrieved using the `/account/bank-details` request. The `merchant_id` used must be a billing or funding level node for the merchant (that holds a bank), otherwise an error with explanation: *"Invalid Merchant ID provided, node is not billing or funding"* will be returned. For billing and funding levels on the subgroup and merchant level, the `internal_mid` for the node may be used.
        
