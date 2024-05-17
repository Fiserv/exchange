---
tags: [Getting Started, Maintenance]
---
# Merchant Maintenance

## Additional Location process

### Creating a new location

The process for adding an additional location is similar to a maintenance case. The user must start by creating an additional location to add to an existing merchant by creating a maintenance type with type "ADD_locationS"

This returns `application_reference` which can be updated.

### Updating the new location

The additional location can then be updated using the `/boarding/outlet/update` endpoint in order to update the application

### Submitting the new location

As this is an application for the location, the location must be submit using the `/boarding/application` [endpoint](../api/?type=post&path=/boarding//application) for submitting an application.

Just like a normal application, if `submit_success` in the response is `1`, the application succesfully submit to the new step in workflow. Checking the status of the application will allow you to verify if this was succesfully boarded. Once boarded, will be added to the existing merchant.
