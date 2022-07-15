# Uploading additional Documents during Risk Screening

## Shared Services Risk Screening process

### In Manual Review / Back to Sales

When using shared services, the user may be asked to provide additional documentation during the credit risk screening process. 
This will occur when an application is being manually reviewed, and may require suppoer documents such as Bank statements or proof of address. 
This response will be sent to Exchange from credit as a 'back to sales' response, with a comment to let the user know why this has occured and what is required.

### Response process

The user will be able to respond to the credit team with the additional documents requested by uploading them and submitting a comment back, 
which will be facilitated through the `/fdapplication/upload_additional_files` , `/fdapplication/upload_additional_documents` and `/boarding/document_categories` endpoints.

#### Retrieving document categories

In order to upload a file, it must be assigned a category to be uploaded to. This will need to have been configured on the configuration portal prior to retrieving. 
The available categories are: 

- Proof of ID
- Proof of Business
- Proof of Adress
- Other

These will have documents grouped within this category during the configuration done.

#### Uploading the files

The files to upload will be sent through the `/fdapplication/upload_additional_files` for the application, and will require the payload to be sent as form-data. 
The form will require two keys, `request` and `file` - where the request is the body and file is an uploaded file. Only one file at a time can be sent through the api

The request must contain the application reference, and the external id of what entity the document is for. 

Example request body:
```
{
    "application": {
        "application_reference": "333020220715,
        "tenant_udc_external_id":"TDC08-23KS2-823JR-72240-34KDF-CAE91-EFB47"
    }
}
```

However, this will be dependant on the configuration of the documents. 
