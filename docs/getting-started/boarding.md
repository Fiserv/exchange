# Boarding

## Boarding by API

Exchange offers end-to-end Boarding through API that is facilitated through Adding Applications, Subgroups and Outlets in order to create the correct Merchant Hierarchy. This includes adding, and updating merchant applications in progress before submitting them.

For the standard *Merchant - Chain - Outlet*  Hierarchy, three calls are needed to submit an application.
This can include pricing and equipment for the Merchant that is required, and the billing and funding settings for the Merchant. \

While an Application is in 'Open' status, this can be updated using the UPDATE requests, of which can be done for each level of the Merchant.
An applications status and information can be retrieved using the APPLICATION_STATUS_CHECK and RETRIEVE_APPLICATION requests, and a complete application can be submit by using the APPLICATION_SUBMIT request (pending validation). 
Applications that are invalid will respond with the errors and their locations so that the entity may be updated, and resubmit. 

