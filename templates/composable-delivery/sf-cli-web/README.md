<!-- summary:start -->
# Salesforce CLI Web Login with Your Own App

`composable-delivery/sf-cli-web` version 0.0.1

Template published by MuseLab (@composable-delivery), included in the official registry reviewed by its maintainers and shipped with this plugin version.

## What this template deploys with its default values

### What is deployed

- App: CliWebLogin
- Sign-in flow: Authorization code (web server): a user signs in through a browser and approves the app.
- Distribution: Local: the app exists in this org only

### Who can use the app

- Users: Decided when the app is deployed, by the admin who deploys it. The plugin recommends admin-approved access: only users who hold a permission set made for the app can use it.
- Session level: Standard: no second factor is required by the app.

### What the app is allowed to do

- Api: Read and change the org's data through the REST, SOAP and Bulk APIs, with the user's own permissions.
- Web: Open the Salesforce user interface and Visualforce pages in a browser as the user.
- RefreshToken: Keep access after the user has left: the app can get new access tokens without the user being present.

### Where authorization codes are sent

- localhost:1717: http://localhost:1717/OauthRedirect (this machine: a program listening on that port receives the code)
- Client: This plugin (sf eca mcp login and sf eca mcp proxy): http://localhost:1717/OauthRedirect

### Client, tokens and network

- Client type: Holds a secret: the consumer secret is needed to turn an authorization code into a token.
- PKCE: Required: an intercepted authorization code cannot be redeemed on its own
- How long access lasts: Refresh tokens expire 30 days after they are issued. Each refresh replaces the refresh token.
- IP restrictions: Enforced: the login IP ranges on users' profiles apply to this app

### Shown to users in the org

- Label: CLI Web Login
- Description: Used by the Salesforce CLI command sf org login web.
- Contact email: ${ADMIN_EMAIL}

## Parameters

- NAME (string, required), default: CliWebLogin
- ADMIN_EMAIL (email, required)
- OAUTH_LOCAL_PORT (integer), default: 1717

## Risks

### In a scratch org

- note: The app can open the Salesforce user interface as the user (web-scope). The Web scope lets the app turn its access token into a browser session in a scratch org, signed in as the user, without the user's password or second factor.
- note: Authorization codes are only ever sent to the local machine (callback-localhost-only). CliWebLogin sends authorization codes for a scratch org to localhost:1717 only. Any program on a user's machine that listens on that port receives the code; PKCE is required, so the code alone is not enough to get a token.

### In a sandbox

- warning: Authorization codes are only ever sent to the local machine (callback-localhost-only). CliWebLogin sends authorization codes for a sandbox to localhost:1717 only. Any program on a user's machine that listens on that port receives the code; PKCE is required, so the code alone is not enough to get a token. A sandbox often holds a copy of production data.
- note: The app can open the Salesforce user interface as the user (web-scope). The Web scope lets the app turn its access token into a browser session in a sandbox, signed in as the user, without the user's password or second factor.

### In a production org

- warning: The app can open the Salesforce user interface as the user (web-scope). The Web scope lets the app turn its access token into a browser session in a production org, signed in as the user, without the user's password or second factor.
- warning: Authorization codes are only ever sent to the local machine (callback-localhost-only). CliWebLogin sends authorization codes for a production org to localhost:1717 only. Any program on a user's machine that listens on that port receives the code; PKCE is required, so the code alone is not enough to get a token.

## Description from MuseLab

- Name: Salesforce CLI Web Login with Your Own App
- Version: 0.0.1
- Says it is for: Salesforce CLI (sf org login web)
- Category: Developer Tools
- Summary: For orgs that do not use Salesforce's default app for 'sf org login web'.
- Description: Salesforce provides a default app for 'sf org login web', so this template is optional. Use it when your org signs in with an app of its own, and pass that app's client id to the command with --client-id.
- Documentation link: https://developer.salesforce.com/docs/platform/sfdx-dev/guide/sfdx-dev-auth-eca.html
- Tags: sf-cli, developer
- Parameter NAME: App API Name: API name for the External Client App in your org, for example CliWebLogin.
- Parameter ADMIN_EMAIL: Administrator Contact Email: Email address of the person responsible for this app.
- Parameter OAUTH_LOCAL_PORT: Local Callback Port: Port the Salesforce CLI listens on for the sign-in response: the oauthLocalPort value in sfdx-project.json, or 1717 when that is not set.
<!-- summary:end -->
