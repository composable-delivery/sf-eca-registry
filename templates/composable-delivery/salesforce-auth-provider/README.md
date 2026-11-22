<!-- summary:start -->
# Salesforce Authentication Provider

`composable-delivery/salesforce-auth-provider` version 0.0.1

Template published by MuseLab (@composable-delivery), included in the official registry reviewed by its maintainers and shipped with this plugin version.

## What this template deploys with its default values

### What is deployed

- App: AuthProviderLogin
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

- Label: Auth Provider Login
- Description: Used by another Salesforce org to sign in to this one through an Authentication Provider.
- Contact email: ${ADMIN_EMAIL}

## Parameters

- NAME (string, required), default: AuthProviderLogin
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

- Name: Salesforce Authentication Provider
- Version: 0.0.1
- Says it is for: Salesforce Authentication Provider
- Category: iPaaS & Automation
- Summary: For the org that another Salesforce org signs in to through a Salesforce Authentication Provider.
- Description: Deploy this app in the identity provider org. The other org's Authentication Provider is then set up with this app's credentials, and shows the callback address this app needs.
- Documentation link: https://help.salesforce.com/s/articleView?id=xcloud.sso_provider_sfdc.htm
- Tags: auth-provider, cross-org
- Parameter NAME: App API Name: API name for the External Client App in the identity provider org, for example AuthProviderLogin.
- Parameter ADMIN_EMAIL: Administrator Contact Email: Email address of the person responsible for this app.
- Parameter CALLBACK_URL: Callback URL: The Callback URL the Authentication Provider shows, copied as it is. The provider needs this app's consumer key first, so deploy once with the address you expect and deploy again with the one it shows [...]
<!-- summary:end -->
