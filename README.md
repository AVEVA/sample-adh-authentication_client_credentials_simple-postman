**Version:** 1.0.0


# OSIsoft Cloud Services Client Authentication Postman Collection

**Version:** 1.0.0

[![Build Status](CCCCCCCCCCCCCCCCC)]

## Requirements

- Postman 
- Register a [Client-Credentials Client](https://cloud.osisoft.com/clients) in your OSIsoft Cloud Services tenant and create a client secret to use in the configuration of this sample. ([Video Walkthrough](https://www.youtube.com/watch?v=JPWy0ZX9niU))
  - __NOTE__: This sample only requires the `Tenant Member` role to run successfully 
    - see: ['Authorization Allowed for these roles' in the documentation](https://docs.osisoft.com/bundle/ocs/page/api-reference/tenant/tenant-tenants.html#get-tenant) 
  - It is strongly advised to not elevate the permissions of a client beyond what is necessary.

## About this sample collection

This sample is meant to be very simple and straightforward to show how you can use common Postman to retrieve a bearer token for authenticating against OCS.

## Configuring the sample

Steps:
1. Import the [collection file](postman_collection.json) to Postman 
1. Select Collections in the left sidebar and edit the imported collection by clicking its title, then under the 'Variables' tab add your client Id and secret to the corresponding variable under the 'Current' column. 
1. Optionally, to test some interactions with the OCS APIs, add your Tenant Id, Namespace Id, and Stream Id to the corresponding variables. This will let you use the authentication token to make calls to OCS.

![Adding Variables](Images/variables.png)

For more information on collection variables, see the [Postman docs](https://learning.postman.com/docs/sending-requests/variables/#defining-collection-variables)

OSIsoft Cloud Services is secured by obtaining tokens from its identity endpoint, retrieved here by calling 'Get Well Known Open ID'. Client credential clients provide an identifier and an associated secret that are authenticated against the token endpoint. Below we will call the 'Get Bearer Token' with the now entered client identifier and secret to retrieve the token.

## Running the sample

To run this collection complete the following steps

1. Execute the 'Get Well Known Open ID' call to get the authorization endpoint to hit when getting the bearer token. (See this value now reflected as a variable 'authorization_endpoint' in the collection, and used as URL for the bearer token call)
1. Execute the 'Get Bearer Token' call, which uses the 'client_id' and 'client_secret' variables to retrieve an authorization token. 
1. See the token returned in the response under the 'access_token' key. A collection variable containing the token should also have been created.
1. Optionally, if you entered Tenant, Namespace, and Stream identifiers mentioned above, execute the remaining 'Get Namespaces', 'Get Streams', and 'Get Data for Stream' calls. To get data you will need to replace the placeholders for start index and count using the Params columns.

![Placeholders](Images/placeholders.png)

To test this sample run
```bash
npm ci
```

then replace the placeholders in [appsettings.placeholder.json](appsettings.placeholder.json) with your values and rename the file to appsettings.json. (The file name appsettings.json is ignored by Git to avoid users accidentally exposing sensitive data) 

Then run
```bash
newman run ./postman_collection.json -d ./appsettings.json
```

---

For the main OSIsoft samples page [ReadMe](https://github.com/osisoft/OSI-Samples)
