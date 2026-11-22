<!-- summary:start -->
# Tableau Server Custom OAuth Client

`composable-delivery/tableau-server` version 0.0.1

Template published by MuseLab (@composable-delivery), included in the official registry reviewed by its maintainers and shipped with this plugin version.

## What this template deploys with its default values

### What is deployed

- App: BiServerLogin
- Sign-in flow: Authorization code (web server): a user signs in through a browser and approves the app.
- Distribution: Local: the app exists in this org only

### Who can use the app

- Users: Decided when the app is deployed, by the admin who deploys it. The plugin recommends admin-approved access: only users who hold a permission set made for the app can use it.
- Session level: Standard: no second factor is required by the app.

### What the app is allowed to do

- OpenID: Learn the user's unique identifier through OpenID Connect and receive an ID token.
- Profile: Read who the user is from the identity service: user id, name, email, address and phone. The org stores it as Basic.
- Email: Read who the user is from the identity service: user id, name, email, address and phone. The org stores it as Basic.
- Address: Read who the user is from the identity service: user id, name, email, address and phone. The org stores it as Basic.
- Phone: Read who the user is from the identity service: user id, name, email, address and phone. The org stores it as Basic.
- Api: Read and change the org's data through the REST, SOAP and Bulk APIs, with the user's own permissions.
- RefreshToken: Keep access after the user has left: the app can get new access tokens without the user being present.

### Where authorization codes are sent

- Host not known yet: https://${TABLEAU_SERVER_FQDN}/auth/add_oauth_token (the host depends on a value that has not been supplied)

### Client, tokens and network

- Client type: Holds a secret: the consumer secret is needed to turn an authorization code into a token.
- PKCE: Required: an intercepted authorization code cannot be redeemed on its own
- How long access lasts: Refresh tokens expire 30 days after they are issued. Each refresh replaces the refresh token.
- IP restrictions: Enforced: the login IP ranges on users' profiles apply to this app

### Shown to users in the org

- Label: BI Server Login
- Description: Used by Tableau Server to connect to Salesforce.
- Contact email: ${ADMIN_EMAIL}

## Parameters

- NAME (string, required), default: BiServerLogin
- ADMIN_EMAIL (email, required)
- TABLEAU_SERVER_FQDN (string, required)

## Risks

### In a scratch org

None reported.

### In a sandbox

None reported.

### In a production org

None reported.

## Description from MuseLab

- Name: Tableau Server Custom OAuth Client
- Version: 0.0.1
- Says it is for: Tableau Server
- Category: Data & Analytics
- Summary: For a Tableau Server that connects to Salesforce with an OAuth client of your own.
- Description: Tableau Server uses a Tableau-managed app by default. Use this template only when you set up your own client; its credentials and redirect address are then entered on the server with 'tsm configuration set'.
- Documentation link: https://help.tableau.com/current/server/en-us/config_oauth_sfdc.htm
- Tags: tableau, analytics
- Parameter NAME: App API Name: API name for the External Client App in your org, for example BiServerLogin.
- Parameter ADMIN_EMAIL: Administrator Contact Email: Email address of the person responsible for this app.
- Parameter TABLEAU_SERVER_FQDN: Tableau Server Host Name: Fully qualified domain name of your Tableau Server, without https://, for example tableau.example.com.
<!-- summary:end -->
