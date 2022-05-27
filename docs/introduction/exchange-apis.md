# Exchange APIs

Exchange offers a full boarding and funding experience avaliable through RESTful API. All requests and response will be sent in the JSON format, and a postman collection is avaliable for integration support *here*

APIs avaliable can be viewed on the 'API Explorer' section, and covers
*  Boarding
*  Funding
 * *Including Funding details and reporting*
* Risk
*  Offerings

API found under boarding will support merchant on-boarding. Exchange allows end-to-end, flexible boarding through our API to create the Merchant Hierarchy desired.
Just like boarding through the UI, validation will return any errors upon submission to let the user know what field and part of the application needs to be updated - which can done through our merchant update API.

Our funding API is avaliable for users who will be using solutions that requires this, such as Instructional funding or Managed split by Transaction.
We offer two funding endpoints for instructional funding, /funding/instruction and /funding/detailed-instruction. These endpoints allow the PayFac to control of the recipient of funds by account type and amount, and the abalility to add detailed breakdown information for reporting on the amounts instructed if desired through the second.

Offerings are avaliable to view and add to merchants through the API. Offerings will contain transaction pricing, equipment, and online products that can be added during boarding. This is mainly used for Managed Funding and to add equipment, where pricing will be added to perform calculations for the PayFac instead of instructions sent via API.

