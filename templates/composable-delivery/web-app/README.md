<!-- summary:start -->
# Web Server Flow Application

`composable-delivery/web-app` version 0.0.1

Template published by MuseLab (@composable-delivery), included in the official registry reviewed by its maintainers and shipped with this plugin version.

## What this template deploys with its default values

### What is deployed

- App: WebApp
- Sign-in flow: Authorization code (web server): a user signs in through a browser and approves the app.
- Distribution: Local: the app exists in this org only

### Who can use the app

- Users: Decided when the app is deployed, by the admin who deploys it. The plugin recommends admin-approved access: only users who hold a permission set made for the app can use it.
- Session level: Standard: no second factor is required by the app.

### What the app is allowed to do

- Api: Read and change the org's data through the REST, SOAP and Bulk APIs, with the user's own permissions.
- RefreshToken: Keep access after the user has left: the app can get new access tokens without the user being present.

### Where authorization codes are sent

- Host not known yet: ${CALLBACK_URL} (the host depends on a value that has not been supplied)

### Client, tokens and network

- Client type: Holds a secret: the consumer secret is needed to turn an authorization code into a token.
- PKCE: Required: an intercepted authorization code cannot be redeemed on its own
- How long access lasts: Refresh tokens expire 30 days after they are issued. Each refresh replaces the refresh token.
- IP restrictions: Enforced: the login IP ranges on users' profiles apply to this app

### Shown to users in the org

- Label: Web Application
- Description: Used by a web application to sign users in with Salesforce.
- Contact email: ${ADMIN_EMAIL}

## Parameters

- NAME (string, required), default: WebApp
- ADMIN_EMAIL (email, required)
- CALLBACK_URL (string, required)

## Risks

### In a scratch org

None reported.

### In a sandbox

None reported.

### In a production org

None reported.

## Description from MuseLab

- Name: Web Server Flow Application
- Version: 0.0.1
- Says it is for: OAuth 2.0 web server flow client
- Category: Custom
- Summary: For a web application with a server-side back end that signs users in to Salesforce.
- Description: Use this template for your own web application whose server code calls Salesforce for the people who sign in to it. Adapt the plan it generates with 'sf eca plan generate' for anything more specific.
- Documentation link: https://help.salesforce.com/s/articleView?id=xcloud.remoteaccess_oauth_web_server_flow.htm
- Tags: web, web-server
- Parameter NAME: App API Name: API name for the External Client App in your org, for example PortalWebApp.
- Parameter ADMIN_EMAIL: Administrator Contact Email: Email address of the person responsible for this app.
- Parameter CALLBACK_URL: Callback URL: Address on your web application that receives the sign-in response from Salesforce, for example https://app.example.com/oauth/callback. An http://localhost address can be used while developing.
<!-- summary:end -->
