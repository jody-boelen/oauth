# OAuth
The OAuth module allows you to easily secure your published REST services (or OData services) with a client credentials flow. It does not contain its own authorization server, but it can verify tokens generated by authorizations servers against that server (using an auth0 java libary to validate the JWT). The module also allows for specifying scopes on PRS level, where you can specify scopes as granular as you like:
- Have scopes for each PRS (no need to check HTTP method or location)
- Have scopes per resource (only check the location)
- Have scopes per resource and operation (check both HTTP method and location)

## Features and limitations

- Add a custom authorization microflow to your API to secure it with OAuth.
- The module already validates the token by default, you are free to add scopes to the validation.
- Currently, the token validation will be done by using a local verification. Introspection is currently not supported due to slightly different introspection implementations per authorization server.
## Dependencies

- Mendix 8.12.7 or higher
- Community Commons Module
- Encryption Module

## Configuration

1. Grant the Administrator/Configurator the Administrator module role
2. Create a page that uses the SNIP_AuthorizationServer_Overview snippet from the USEME module
3. Copy the PRS_Auth_Custom microflow into your own module and use this as custom auth flow for your API.
4. In the custom auth microflow, add a string header parameter 'Authorization'.
5. Modify the copied PRS_Auth_Custom microflow to suit your needs:
   - Copy and change SUB_Request_FindRequiredScope to add required scopes for the PRS, these will be evaluated each time a user calls the endpoint. You can use the example implementation as a reference, here scopes are defined on an endpoint level.
   - Change SUB_Client_FindOrCreate to point towards the correct API user userrole in your app (WILL PROBABLY GIVE AN ERROR UPON DOWNLOADING THE MODULE, due to a non-present user role).
6. After deploying the app, add your authorization server via the snippet, you can do this manually or you can simply use the well-known url to fill in all the details.
7. You are ready to use the module.
8. (Exclude the example PRS as this serves no further use)

