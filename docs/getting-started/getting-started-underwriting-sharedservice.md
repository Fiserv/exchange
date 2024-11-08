---
tags: [Getting Started, Underwriting, Risk, Application]
---

# Shared Service 

The shared service model utilises a decision coming back from Risk. The flow of the application may change depending on the decision sent. 
Below is a process flow for an application going through the Risk service in a shared service model.

<!-- !align: center -->
![<img src="risk_sequence.png" width="600"/>](/assets/images/shared_service_flow.png)

## More info required flow

When using shared services, the user may be asked to provide additional documentation and/or information during the credit risk screening process. 
This will occur when an application is being manually reviewed.
### In Manual Review / Back to Sales

This response will be sent to Exchange from credit as a 'Back to Sales' response, with a comment to let the user know why this has occurred and what is required.
This will be checked by retrieving the merchant applications information through the 'RETRIEVE_MERCHANT_HIERARCHY' endpoint, where the `"credit_risk_check_response"` block will contain the current credit risk check info for the application. A `"decision": "MORE_INFO_REQUIRED"` indicates that the back to sales message has been received and is ready to be processed, where the risk reviewers comment `"credit_risk_comments":` can be viewed in order to know what is being requested.

### Response process

The user will be able to respond to the credit team with the additional documents and information requested by uploading them and submitting a comment back, 
which will be facilitated through the `/fdapplication/upload_additional_files` , `/fdapplication/submit_additional_documents` and `/boarding/document_categories` endpoints.

### Retrieving document categories

<!-- theme: info -->
>**POST** `/boarding/document_categories`

In order to upload a file, it must be assigned a category to be uploaded to. This will need to have been configured on the configuration portal prior to retrieving. 
The available categories are: 

- Proof of ID
- Proof of Business
- Proof of Address
- Proof of Bank
- Other

These will have documents grouped within this category during the configuration done. The `tenant_udc_external_id` will be returned for the categories displayed.

### Uploading the files

<!-- theme: info -->
>**POST** `/fdapplication/upload_additional_files`

The files to upload will be sent through the `/fdapplication/upload_additional_files` for the application reference stated, and will require the payload to be sent as form-data. 
The form will require two keys, `request` and `file` - where the request is the body and file is an uploaded binary file. Only one file at a time can be sent through the API.

The request must contain the application reference, and the external id of what entity the document is for.

Example request body:
```
{
    "application": {
        "application_reference": "333020220715",
        "tenant_udc_external_id": "TDC08-23KS2-823JR-72240-34KDF-CAE91-EFB47"
    }
}
```

However, this request body will be dependent on the configuration of the documents. If mandatory meta data has been configured for the document, this must be added in the request body under a `document_data` object, seen below.

```
{
    "application": {
        "application_reference": "333020220715",
        "tenant_udc_external_id": "TDC08-23KS2-823JR-72240-34KDF-CAE91-EFB47"
    },
    "document_data": {
        "first_name": "Test",
        "second_name": "Test",
        "sur_name": "Test",
        "date_of_birth": "1998/10/24",
        "document_id": "CWR442DF2FD",
        "issued_date": "2022/06/10",
        "expiry_date": "2032/06/10",
        "document_issuer": "Test",
        "issuing_state": "CA",
        "issuing_country": "840"
    }
}
```
### Submitting the documents

<!-- theme: info -->
>**POST** `/fdapplication/submit_additional_documents`

After all the files have been uploaded that have been requested, the user may now submit the documents to Exchange along with any responses to additional information requests for the risk reviewer to see.
```
{
    "operation": {
        "operation_type": "APPLICATION_SUBMIT_ADDITIONAL_DOCUMENTS",
        "version": "2.0.0"
    },
    "application": {
        "application_reference": "333020220715"
    },
    "note": "Please see additional documents, with statement from January as requested."
}
```
## Submission Errors

<!-- theme: info -->
>**POST** `/boarding/application`

After an application is submitted , it will move to underwriting. If there are any situations where a Credit Risk Error or AML Error is received due to invalid data, an application can be unlocked using the unlock application endpoint. The application can then be submitted using the submit application endpoint.

```json
{
  "operation": {
    "operation_type": "APPLICATION_UNLOCK"
  },
  "application": {
    "application_external_id": "APL01-75CDF-663EB-79CBA-DF321-BEUIP-KL123"
  }
}
```
