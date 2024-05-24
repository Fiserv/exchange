# Shared Service 

## Shared Services Back to Sales Flow

When using shared services, the user may be asked to provide additional documentation during the credit risk screening process. 
This will occur when an application is being manually reviewed, and may require supporting documents such as Bank statements or proof of address. 

### In Manual Review / Back to Sales

This response will be sent to Exchange from credit as a 'back to sales' response, with a comment to let the user know why this has occured and what is required.
This will be checked by retrieving the merchant applications information through `/boarding/application` operation `'RETRIEVE_MERCHANT_HIERARCHY'` , where the `"credit_risk_check_response"` block will contain the current credit risk check info for the application. A `"decision": "MORE_INFO_REQUIRED"` indicates that the back to sales message has been recieved and is ready to be processed, where the risk reviewers comment `"credit_risk_comments":` can be viewed in order to know what is required to upload.

### Response process

The user will be able to respond to the credit team with the additional documents requested by uploading them and submitting a comment back, 
which will be facilitated through the `/fdapplication/upload_additional_files` , `/fdapplication/submit_additional_documents` and `/boarding/document_categories` endpoints.

### Retrieving document categories

<!-- theme: info -->
>**POST** `/boarding/document_categories`

In order to upload a file, it must be assigned a category to be uploaded to. This will need to have been configured on the configuration portal prior to retrieving. 
The available categories are: 

- Proof of ID
- Proof of Business
- Proof of Address
- Other

These will have documents grouped within this category during the configuration done. The `tenant_udc_external_id` will be returned for the categories displayed.

### Uploading the files

<!-- theme: info -->
>**POST** `/fdapplication/upload_additional_files`

The files to upload will be sent through the `/fdapplication/upload_additional_files` for the application application reference stated, and will require the payload to be sent as form-data. 
The form will require two keys, `request` and `file` - where the request is the body and file is an uploaded file. Only one file at a time can be sent through the api

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

However, this request body will be dependant on the configuration of the documents. If mandatory meta data has been configured for the document, this must be added in the request body under a `document_data` object, seen below.

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

After all the files have been uploaded that have been requested, the user may now submit the documents to Exchange along with a note for the risk reviewer to see when viewing the documents. This can be used to talk to the credit risk reviewer.
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

After an application is submit, it will move to underwriting. If there are every cases where a Credit Risk Error or AML error is recieved due to invalid data, an application can be unlocked in order to be updated and resubmit using the unlock application endpoint

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
