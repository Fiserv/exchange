# Offerings


## Pricing and Equipment
Exchange supports pricing and equipment added to Applications through the use of offerings. Offerigs are split into three types: Processsing, Equipment and Online. These offerings are created by the PayFac and added to an Offer Package, which can then be retrieved from the `/offering/avaliable` endpoint. Upon retrieving an Offer Package, the offerings avaliable will be listed. Online and Equipment offerings can be retrieved by using the `/offering/equipment` endpoint. A selected Offering (by external ID) can have detals grabbed in order to retrieve the pricing information and equipment information.

Processing offerings (that contain transaction pricing and acquiring charges) may be retrieved by using the `/offering/processing` endpoint and providing the desired external ID. 
Processing offerings will be added to the Merchants **pricing level**, and equipment/online offerings at the outlet.
