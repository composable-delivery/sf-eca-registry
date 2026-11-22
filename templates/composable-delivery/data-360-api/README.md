<!-- summary:start -->
# Data 360 (Data Cloud) API

`composable-delivery/data-360-api` version 0.0.1

Template published by MuseLab (@composable-delivery), included in the official registry reviewed by its maintainers and shipped with this plugin version.

## What this template deploys with its default values

### What is deployed

- App: Data360ApiIntegration
- Sign-in flow: JWT bearer: nobody signs in. The app proves itself with a private key and names the user it acts as.
- Distribution: Local: the app exists in this org only

### Who can use the app

- Users: Decided when the app is deployed, by the admin who deploys it. The plugin recommends admin-approved access: only users who hold a permission set made for the app can use it.
- Login: None. Whoever holds the app's private key can act as any pre-authorized user without a password, a second factor or a login screen.
- Session level: Standard: no second factor is required by the app.

### What the app is allowed to do

- Api: Read and change the org's data through the REST, SOAP and Bulk APIs, with the user's own permissions.
- RefreshToken: Keep access after the user has left: the app can get new access tokens without the user being present.
- CDPIngest: Send data into Data Cloud through the Ingestion API.
- CDPProfile: Read customer profiles from Data Cloud.
- CDPQuery: Run SQL queries against Data Cloud.

### Where authorization codes are sent

- login.salesforce.com: https://login.salesforce.com/services/oauth2/success (site salesforce.com)
- Use: This flow does not redirect anyone, but the org stores these URLs as the app's redirect targets.

### Client, tokens and network

- Client type: No consumer secret is used. The private key identifies the app.
- Certificate: A 2048-bit key pair and a self-signed certificate valid 365 days are generated on this machine, unless a key for this app already exists here.
- How long access lasts: Refresh tokens expire 30 days after they are issued.
- IP restrictions: Enforced: the login IP ranges on users' profiles apply to this app

### Certificate

- Common name (CN): Data360ApiIntegration (default)
- Organization (O): Data360ApiIntegration (default)
- Key: RSA 2048-bit (default)
- Valid for: 365 days (default)
- Signature: SHA-256 with RSA (default)

### Shown to users in the org

- Label: Data 360 API Integration
- Description: Used by a server-side integration to work with Data 360 (Data Cloud).
- Contact email: ${ADMIN_EMAIL}

## Parameters

- NAME (string, required), default: Data360ApiIntegration
- ADMIN_EMAIL (email, required)

## Risks

### In a scratch org

- note: The private key is enough to act as a user (jwt-key-holder-acts-as-users). Whoever holds the private key of Data360ApiIntegration can get a token as a pre-authorized user without a password, a second factor or a login screen. Any user an admin later pre-authorizes in a scratch org can be impersonated this way.

### In a sandbox

- note: The private key is enough to act as a user (jwt-key-holder-acts-as-users). Whoever holds the private key of Data360ApiIntegration can get a token as a pre-authorized user without a password, a second factor or a login screen. Any user an admin later pre-authorizes in a sandbox can be impersonated this way.

### In a production org

- warning: The private key is enough to act as a user (jwt-key-holder-acts-as-users). Whoever holds the private key of Data360ApiIntegration can get a token as a pre-authorized user without a password, a second factor or a login screen. Any user an admin later pre-authorizes in a production org can be impersonated this way.

## Description from MuseLab

- Name: Data 360 (Data Cloud) API
- Version: 0.0.1
- Says it is for: Data 360 (Data Cloud) APIs
- Category: Data & Analytics
- Summary: For a server-side integration that sends data to, or queries, Data 360 (Data Cloud) through its APIs.
- Description: Connects a backend job or service to the Data 360 Ingestion, Profile and Query APIs. It signs in with a JWT, so no person has to be present.
- Documentation link: https://developer.salesforce.com/docs/data/data-cloud-dev/guide/dc-quick-start.html
- Tags: data-360, data-cloud, ingestion, query
- Parameter NAME: App API Name: API name for the External Client App in your org, for example Data360ApiIntegration.
- Parameter ADMIN_EMAIL: Administrator Contact Email: Email address of the person responsible for this app.
<!-- summary:end -->
