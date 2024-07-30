---
tags: [Getting Started, Maintenance]
---
# Merchant Maintenance

## Additional Location process

Additional locations work by Creating a maintenance case, which in turn generates a new 'application' that will need the outlet to be added to it and submitted, similar to the normal application flow. 

### Creating a new location

<!-- theme: info -->
>**POST** `/maintenance`

The process for adding an additional location is similar to a maintenance case. The user must start by creating an additional location to add to an existing merchant by creating a maintenance type with type "ADD_OUTLETS"

This returns `application_reference` which can have the oulet added to it. 

### Adding the new location

<!-- theme: info -->
>**POST** `/boarding/outlet/add`

Adding the location to the outlet is the same as adding the original outlet to an application, and uses the `/boarding/outlet/add` endpoint. The application reference required to be used is returned when creating the maintenance case, and the user should specify the `parent_mid` of the outlet like the standard boarding process. Typically, this will be the subgroup of the application.

### Updating the new location

<!-- theme: info -->
>**POST** `/boarding/outlet/update`


If you need to update the outlet information after you added it (but before submission), the location can then be updated using the `/boarding/outlet/update` like the standard process.

### Submitting the new location

<!-- theme: info -->
>**POST** `/boarding/application`

As this is an application for the location, the location must be submit using the `/boarding/application` [endpoint](../api/?type=post&path=/boarding//application) for submitting an application.

Just like a normal application, if `submit_success` in the response is `1`, the application succesfully submit to the new step in workflow. Checking the status of the application will allow you to verify if this was succesfully boarded. Once boarded, will be added to the existing merchant, and the maintenance case closed.
