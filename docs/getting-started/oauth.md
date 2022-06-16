# OAuth

To generate token for authorisation, the 	`/oauth/token` endpoint may be used, and credentials must be sent as a Basic Auth Header with the request.

# Postman

## Importing

The Postman collection for Exchange can be imported via link or file, by clicking 'import'. Please see the sample collection for Exchange [here](https://www.getpostman.com/collections/8ccc7b5124bb99c89a54)

![postman](/assets/images/import_postman.png)

## Authentication
If testing using postman, the Auth tab can be used to authorise API requests. This can be done by using Auth type Outh 2.0, selecting Grant Type 'Client Credentials', entering the Access Token URL (URL/oauth/token), Client ID as as username an Client secret as password and getting new access token. It may be useful to create an environment in postman and use these as variables.

![postman auth](/assets/images/auth_postman.png)

