# Introduction

## What is Exchange?

The aim of Exchange was to create an end-to-end digital solution for Payment Facilitators and Marketplaces, that allows for integrations of sub-merchant onboarding, reporting, risk decisioning and settlements all in the same platform. Exchange offers two main touchpoints through it's user interface 'Portals' and through API integration.

### Sub-merchants boarding configuration avaliable

The PayFac is able to control configuration of the sub-merchant journey through use of the configuration portal. This initial configuration is done through the user interface  and configurations that are setup are used (such as defaults) for API integration. This can allow for a more fluid on-boarding experience for users who have a similar demographic for the merchants being onboarded that may share or default to certain settings and fields.

Exchange allows applications that have been started and in `open` status to be modified at all sub-merchants hierarchy levels, and these can be submitted by using the application submit request at endpoint `/boarding/application`when ready. Applications do not expire or stagnate, and can be left and submit whenever the PayFac desired.

### OFAC checks and Credit risk checks

After initial configurations, OFAC and Credit risk checks can be included in the flow for merchants boarded by API and decisions can be reviewed and overwritten, and accepted (where applicable) by API request. 

### Relevant content: 

- [Onboarding](?path=docs/getting-started/boarding.md)
- [Ofac and Risk](?path=docs/getting-started/risk.md)
