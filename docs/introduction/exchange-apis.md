# Exchange APIs

## What does Exchange offer? 

Exchange offers a end-to-end sub-merchant on-boarding and funding experience avaliable through RESTful API. All requests and response will be sent in the JSON format, and link to postman collection is avaliable to download for integration support in the 'API Explorer' section.

## What is avaliable?

APIs avaliable can be viewed on the API Explorer, and cover:
- Sub-merchant on-boarding
- Funding 
- Reporting
- OFAC and Credit Risk
- Equipment and Pricing offerings 

These are explained briefly below, where additional API sections can be expanded on the right for more info and full API spec seen in the API explorer.

### Sub-merchant on-boarding 

API found under boarding will support sub-merchant on-boarding. Exchange allows end-to-end, flexible boarding through our API to create the sub-merchant hierarchy desired.
Just like boarding through the UI, validation will return any errors upon submission to let the user know what field and part of the application needs to be updated - which can done through our merchant update API.

### Funding  

Our funding API is avaliable for users who will be using solutions that requires this, such as Instructional funding or Managed split by Transaction.
We offer two funding endpoints for instructional funding, `/funding/instruction` and `/funding/detailed-instruction`. These endpoints allow the PayFac to control of the recipient of funds by account type and amount, and the ability to add detailed breakdown information for reporting on the amounts instructed if desired through the second.

### Reporting

Exchange offers reporting through the use of settlements and segregation of funds through virtual accounts, which can be retrieved by API with the `/settlement/rejects` and `/account/settlement-info` for more information please see the reporting section in additional API info.

### Equipment and Pricing offerings  

Offerings are avaliable to view and add to merchants through the API. Offerings will contain transaction pricing, equipment, and online products that can be added during boarding. This is primarily used for the *Managed Funding* to add equipment and pricing, where pricing will perform calculations for the PayFac instead of instructions sent via API.

