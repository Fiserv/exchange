# Introduction

## What is Exchange?

The aim of Exchange was to create an end-to-end digital solution for Payment Facilitators and Marketplaces, that allows for integrations of sub-merchant onboarding, reporting, risk decisioning and settlements all in the same platform. Exchange offers two main touchpoints through it's user interface 'Portals' and through API integration.

### Sub-merchant boarding configuration avaliable

The PayFac is able to control configuration of the sub-merchant boarding journey through use of the configuration portal. This initial configuration is done through the user interface  and configurations that are setup are used (such as defaults) for API integration. This can allow for a more fluid on-boarding experience for users who have a similar demographic for the sub-merchants being onboarded that may share or default to certain settings and fields.

Exchange allows applications that have been started and in `open` status to be modified at all merchants hierarchy levels, and these can be submitted by using the application submit request at endpoint `/boarding/add_application`when ready. Applications do not expire or stagnate, and can be left and submit whenever the PayFac desired.

### OFAC checks and Credit risk checks

After initial configurations, OFAC and Credit risk checks can be included in the flow for merchants boarded by API and decisions can be reviewed and overwritten, and accepted (where applicable) by API request. 

## Exchange APIs

## What is avaliable?

APIs avaliable can be viewed on the API Explorer, and cover:
- Sub-merchant on-boarding
- Funding 
- Reporting
- OFAC and Credit Risk
- Equipment and Pricing offerings
- Transaction Monitoring

These are explained briefly below, where additional API sections can be expanded on the lefthand side for more info and full API spec seen in the API explorer.

### Sub-merchant on-boarding 

API found under boarding will support sub-merchant on-boarding. Exchange allows flexible boarding through our API to create the sub-merchant hierarchy desired.
Just like boarding through the UI, validation will return any errors upon submission to let the user know what field and part of the application needs to be updated - which can done through our merchant update API.

### Funding  

Our funding API is avaliable for users who will be using solutions that requires this, such as Instructional funding or Managed split by Transaction.
We offer two funding endpoints for instructional funding, `/funding/instruction` and `/funding/detailed-instruction`. These endpoints allow the PayFac to control the recipient of funds by account type and amount, and the ability to add detailed breakdown information for reporting on the amounts instructed if desired through the `detailed-instruction` endpoint.

### Reporting

Exchange offers reporting through the use of settlements and segregation of funds through virtual accounts, which can be retrieved by API with the `/settlement/rejects` and `/account/settlement-info` for more information please see the reporting section in additional API info.

### Equipment and Pricing offerings  

Offerings are avaliable to view and add to sub-merchants through the API. Offerings will contain transaction pricing, equipment, and online products that can be added during boarding. This is primarily used for the *Managed Funding* to add equipment and pricing, where pricing will perform calculations for the PayFac instead of instructions sent via API, but is also used to send entitlements. Test

