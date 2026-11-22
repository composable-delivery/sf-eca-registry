<!-- summary:start -->
# Salesforce CLI JWT Login

`composable-delivery/sf-cli-jwt` version 0.0.1

Template published by MuseLab (@composable-delivery), included in the official registry reviewed by its maintainers and shipped with this plugin version.

## What this template deploys with its default values

### What is deployed

- App: CliJwtLogin
- Sign-in flow: JWT bearer: nobody signs in. The app proves itself with a private key and names the user it acts as.
- Distribution: Local: the app exists in this org only

### Who can use the app

- Users: Decided when the app is deployed, by the admin who deploys it. The plugin recommends admin-approved access: only users who hold a permission set made for the app can use it.
- Login: None. Whoever holds the app's private key can act as any pre-authorized user without a password, a second factor or a login screen.
- Session level: Standard: no second factor is required by the app.

### What the app is allowed to do

- Api: Read and change the org's data through the REST, SOAP and Bulk APIs, with the user's own permissions.
- Web: Open the Salesforce user interface and Visualforce pages in a browser as the user.
- RefreshToken: Keep access after the user has left: the app can get new access tokens without the user being present.

### Where authorization codes are sent

- localhost:1717: http://localhost:1717/OauthRedirect (this machine: a program listening on that port receives the code)
- Client: This plugin (sf eca mcp login and sf eca mcp proxy): http://localhost:1717/OauthRedirect
- Use: This flow does not redirect anyone, but the org stores these URLs as the app's redirect targets.

### Client, tokens and network

- Client type: No consumer secret is used. The private key identifies the app.
- Certificate: A 2048-bit key pair and a self-signed certificate valid 365 days are generated on this machine, unless a key for this app already exists here.
- How long access lasts: Refresh tokens expire 30 days after they are issued.
- IP restrictions: Enforced: the login IP ranges on users' profiles apply to this app

### Certificate

- Common name (CN): CliJwtLogin (default)
- Organization (O): CliJwtLogin (default)
- Key: RSA 2048-bit (default)
- Valid for: 365 days (default)
- Signature: SHA-256 with RSA (default)

### Shown to users in the org

- Label: CLI JWT Login
- Description: Used by the Salesforce CLI command sf org login jwt.
- Contact email: ${ADMIN_EMAIL}

## Parameters

- NAME (string, required), default: CliJwtLogin
- ADMIN_EMAIL (email, required)

## Risks

### In a scratch org

- note: The app can open the Salesforce user interface as the user (web-scope). The Web scope lets the app turn its access token into a browser session in a scratch org, signed in as the user, without the user's password or second factor.
- note: The private key is enough to act as a user (jwt-key-holder-acts-as-users). Whoever holds the private key of CliJwtLogin can get a token as a pre-authorized user without a password, a second factor or a login screen. Any user an admin later pre-authorizes in a scratch org can be impersonated this way.

### In a sandbox

- note: The app can open the Salesforce user interface as the user (web-scope). The Web scope lets the app turn its access token into a browser session in a sandbox, signed in as the user, without the user's password or second factor.
- note: The private key is enough to act as a user (jwt-key-holder-acts-as-users). Whoever holds the private key of CliJwtLogin can get a token as a pre-authorized user without a password, a second factor or a login screen. Any user an admin later pre-authorizes in a sandbox can be impersonated this way.

### In a production org

- warning: The app can open the Salesforce user interface as the user (web-scope). The Web scope lets the app turn its access token into a browser session in a production org, signed in as the user, without the user's password or second factor.
- warning: The private key is enough to act as a user (jwt-key-holder-acts-as-users). Whoever holds the private key of CliJwtLogin can get a token as a pre-authorized user without a password, a second factor or a login screen. Any user an admin later pre-authorizes in a production org can be impersonated this way.

## Description from MuseLab

- Name: Salesforce CLI JWT Login
- Version: 0.0.1
- Says it is for: Salesforce CLI (sf org login jwt)
- Category: CI/CD & DevOps
- Summary: For signing in to an org with 'sf org login jwt', for example from a CI job, with no person present.
- Description: Use this template for any job or machine that runs Salesforce CLI commands against an org with 'sf org login jwt'. That command requires an External Client App of your own.
- Documentation link: https://developer.salesforce.com/docs/platform/sfdx-dev/guide/sfdx-dev-auth-jwt-flow.html
- Tags: sf-cli, jwt, ci
- Parameter NAME: App API Name: API name for the External Client App in your org, for example CliJwtLogin.
- Parameter ADMIN_EMAIL: Administrator Contact Email: Email address of the person responsible for this app.
<!-- summary:end -->
