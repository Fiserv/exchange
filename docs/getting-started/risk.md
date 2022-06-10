# Risk services

## Risk services available in Exchange

If using Risk services in Exchange the PayFac will be able enable Credit risk and OFAC Screening, as well as OFAC monitoring for the Merchant. 
The PayFac will be responsible for reviewing any possible matches retrieved at the business and pricinipal levels to ensure that there is not match with the OFAC list. If an OFAC hit is confirmed, the merchant cannot be boarded and if already on the system will be held from funding.
 
## Screening

After intial configurations have be done to setup screening, the PayFac will be able to retrieve reports that are generated during the boarding process for their merchants by API. The PayFac will also be able to overwrite the decision generated, and process the reports for potential matches.

### OFAC screening API

#### Retrieve intelligence reports available

The `/intelligence/retrieve_intelligence` endpoint can be used to retrieve all avaliable screening reports for a merchant application. This will include the business level, and the principal level. Each entry in the response will return an `entity_reference` to use in the `/intelligence/retrieve_report`.

#### Retrieve intelligence reports

After retrieving the `entity_reference` from  the `/intelligence/retrieve_intelligence` endpoint, the PayFac can then view each report through the `/intelligence/retrieve_report` endpoint.


### Credit risk screening API

## Monitoring

