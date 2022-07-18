# Uploading additional Documents during Risk Screening

## Shared Services Risk Screening process

### In Manual Review / Back to Sales

When using shared services, the user may be asked to provide additional documentation during the credit risk screening process. 
This will occur when an application is being manually reviewed, and may require suppoer documents such as Bank statements or proof of address. 
This response will be sent to Exchange from credit as a 'back to sales' response, with a comment to let the user know why this has occured and what is required.

### Response process

The user will be able to respond to the credit team with the additional documents requested by uploading them and submitting a comment back, 
which will be facilitated through the `/fdapplication/upload_additional_files` , `/fdapplication/submit_additional_documents` and `/boarding/document_categories` endpoints.

#### Retrieving document categories

In order to upload a file, it must be assigned a category to be uploaded to. This will need to have been configured on the configuration portal prior to retrieving. 
The available categories are: 

- Proof of ID
- Proof of Business
- Proof of Address
- Other

These will have documents grouped within this category during the configuration done. The `tenant_udc_external_id` will be returned for the categories displayed.

#### Uploading the files

The files to upload will be sent through the `/fdapplication/upload_additional_files` for the application application reference stated, and will require the payload to be sent as form-data. 
The form will require two keys, `request` and `file` - where the request is the body and file is an uploaded file. Only one file at a time can be sent through the api

The request must contain the application reference, and the external id of what entity the document is for. ### MEtA Datata mandatory... populate request

Example request body:
```
{
    "application": {
        "application_reference": "333020220715",
        "tenant_udc_external_id": "TDC08-23KS2-823JR-72240-34KDF-CAE91-EFB47"
    }
}
```

However, this will be dependant on the configuration of the documents. If mandatory meta data has been configured for the document, this must be added in the request body under a `document_data` object.

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
#### Submitting the documents

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

After submitting the documents, Exchange will notify the credit reviewer in order to view the documents. After these have been reviewed and processed, the credit risk process will proceed or may require additional documents again to proceed.
