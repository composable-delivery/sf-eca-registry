<!-- summary:start -->
# Agentforce Models API Client

`composable-delivery/agentforce-models-api` version 0.0.1

Template published by MuseLab (@composable-delivery), included in the official registry reviewed by its maintainers and shipped with this plugin version.

## What this template deploys with its default values

### What is deployed

- App: ModelsApiClient
- Sign-in flow: Client credentials: nobody signs in. The app proves itself with its consumer key and secret and every token acts as one run-as user.
- Distribution: Local: the app exists in this org only

### Who can use the app

- Users: Decided when the app is deployed, by the admin who deploys it. The plugin recommends admin-approved access: only users who hold a permission set made for the app can use it.
- Run-as user: Not named yet. The admin who deploys the app names the user with --run-as, and every access token acts as that user.
- Login: None. Nobody signs in: the app gets its tokens with its consumer key and secret. Salesforce warns: "With this flow enabled, any person or app that has access to your external client app's consumer key and consumer secret can get an access token."
- Assigned to the run-as user: No. Nobody holds these permission sets until they are assigned
- Session level: Standard: no second factor is required by the app.

### What the app is allowed to do

- Api: Read and change the org's data through the REST, SOAP and Bulk APIs, with the user's own permissions.
- SFApiPlatform: Call Salesforce API Platform services, which the Agent API and hosted MCP servers are served from.

### Where authorization codes are sent

- localhost:1717: http://localhost:1717/OauthRedirect (this machine: a program listening on that port receives the code)
- Origin: The plan names no callback URL, so the plugin writes the one above.
- Client: This plugin (sf eca mcp login and sf eca mcp proxy): http://localhost:1717/OauthRedirect
- Use: This flow does not redirect anyone, but the org stores these URLs as the app's redirect targets.

### Client, tokens and network

- Client type: Holds a secret: the consumer key and secret are the whole credential. Whoever holds both can get a token as the run-as user.
- Token request: A POST to the org's My Domain URL at /services/oauth2/token with grant_type=client_credentials. The org does not accept the request at login.salesforce.com or test.salesforce.com.
- How long access lasts: Until the access token expires. No refresh token scope is granted, so the app cannot renew it.
- Access tokens: JWTs, valid as long as the user's session setting allows. A JWT cannot be revoked before it expires.
- IP restrictions: Enforced: the login IP ranges on users' profiles apply to this app

### Settings that differ from the defaults

- oauth.isNamedUserJwtEnabled: true (default: false). Reference from MuseLab: https://developer.salesforce.com/docs/ai/agentforce/guide/models-api-authentication.html

### Shown to users in the org

- Label: Models API Client
- Description: Used by a server-side program to call the Agentforce Models API.
- Contact email: ${ADMIN_EMAIL}

## Parameters

- NAME (string, required), default: ModelsApiClient
- ADMIN_EMAIL (email, required)

## Risks

### In a scratch org

- note: The consumer key and secret are enough to act as a user (client-credentials-secret-acts-as-user). Nobody signs in to ModelsApiClient. Whoever holds its consumer key and consumer secret can get an access token as its run-as user in a scratch org, with no password, second factor or login screen. Salesforce says: "With this flow enabled, any person or app that has access to your external client app's consumer key and consumer secret can get an access token."

### In a sandbox

- warning: The consumer key and secret are enough to act as a user (client-credentials-secret-acts-as-user). Nobody signs in to ModelsApiClient. Whoever holds its consumer key and consumer secret can get an access token as its run-as user in a sandbox, with no password, second factor or login screen. Salesforce says: "With this flow enabled, any person or app that has access to your external client app's consumer key and consumer secret can get an access token." A sandbox often holds a copy of production data.

### In a production org

- high: The consumer key and secret are enough to act as a user (client-credentials-secret-acts-as-user). Nobody signs in to ModelsApiClient. Whoever holds its consumer key and consumer secret can get an access token as its run-as user in a production org, with no password, second factor or login screen. Salesforce says: "With this flow enabled, any person or app that has access to your external client app's consumer key and consumer secret can get an access token."

## Description from MuseLab

- Name: Agentforce Models API Client
- Version: 0.0.1
- Says it is for: Agentforce Models API
- Category: AI & Agents
- Summary: For a server-side program that calls large language models through the Agentforce Models API, with no person present.
- Description: Connects a backend program to the Agentforce Models API. Nobody signs in: the admin who deploys the app chooses the Salesforce user the program runs as, with --run-as.
- Documentation link: https://developer.salesforce.com/docs/ai/agentforce/guide/models-api-authentication.html
- Tags: agentforce, models-api, ai
- Parameter NAME: App API Name: API name for the External Client App in your org, for example ModelsApiClient.
- Parameter ADMIN_EMAIL: Administrator Contact Email: Email address of the person responsible for this app.
<!-- summary:end -->
