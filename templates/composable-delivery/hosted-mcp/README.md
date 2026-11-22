<!-- summary:start -->
# Salesforce Hosted MCP Server Client

`composable-delivery/hosted-mcp` version 0.0.1

Template published by MuseLab (@composable-delivery), included in the official registry reviewed by its maintainers and shipped with this plugin version.

## What this template deploys with its default values

### What is deployed

- App: SalesforceHostedMcp
- Sign-in flow: Authorization code (web server): a user signs in through a browser and approves the app.
- Distribution: Local: the app exists in this org only

### Who can use the app

- Users: Decided when the app is deployed, by the admin who deploys it. The plugin recommends admin-approved access: only users who hold a permission set made for the app can use it.
- Session level: Standard: no second factor is required by the app.

### What the app is allowed to do

- MCP: Use Salesforce Hosted MCP Servers: call the tools those servers expose, as the user.
- RefreshToken: Keep access after the user has left: the app can get new access tokens without the user being present.

### Where authorization codes are sent

- localhost:1717: http://localhost:1717/OauthRedirect (this machine: a program listening on that port receives the code)
- Client: This plugin (sf eca mcp login and sf eca mcp proxy): http://localhost:1717/OauthRedirect

### Client, tokens and network

- Client type: Public client: no consumer secret. Anyone who knows the consumer key can start a login.
- PKCE: Required: an intercepted authorization code cannot be redeemed on its own
- How long access lasts: Refresh tokens expire 30 days after they are issued. Each refresh replaces the refresh token.
- Access tokens: JWTs, valid as long as the user's session setting allows. A JWT cannot be revoked before it expires.
- IP restrictions: Enforced: the login IP ranges on users' profiles apply to this app

### Settings that differ from the defaults

- oauth.isConsumerSecretOptional: true (default: false). Reference from MuseLab: https://developer.salesforce.com/docs/platform/hosted-mcp-servers/guide/claude.html
- oauth.isNamedUserJwtEnabled: true (default: false). Reference from MuseLab: https://developer.salesforce.com/docs/platform/hosted-mcp-servers/guide/create-external-client-app.html

### Shown to users in the org

- Label: Salesforce MCP: This plugin
- Description: Used by MCP clients to connect to the Hosted MCP servers run by Salesforce.
- Contact email: ${ADMIN_EMAIL}

## Parameters

- NAME (string, required), default: SalesforceHostedMcp
- ADMIN_EMAIL (email, required)
- MCP_CLIENTS (mcp-clients, required), default: sf-eca

## Risks

### In a scratch org

- note: Authorization codes are only ever sent to the local machine (callback-localhost-only). SalesforceHostedMcp sends authorization codes for a scratch org to localhost:1717 only. Any program on a user's machine that listens on that port receives the code; PKCE is required, so the code alone is not enough to get a token.

### In a sandbox

- warning: Authorization codes are only ever sent to the local machine (callback-localhost-only). SalesforceHostedMcp sends authorization codes for a sandbox to localhost:1717 only. Any program on a user's machine that listens on that port receives the code; PKCE is required, so the code alone is not enough to get a token. A sandbox often holds a copy of production data.

### In a production org

- warning: Authorization codes are only ever sent to the local machine (callback-localhost-only). SalesforceHostedMcp sends authorization codes for a production org to localhost:1717 only. Any program on a user's machine that listens on that port receives the code; PKCE is required, so the code alone is not enough to get a token.

## Description from MuseLab

- Name: Salesforce Hosted MCP Server Client
- Version: 0.0.1
- Says it is for: Salesforce Hosted MCP Servers
- Category: AI & Agents
- Summary: For connecting an MCP client, such as Claude, ChatGPT or Cursor, to a Salesforce hosted MCP server.
- Description: Use this template for one MCP client, or for several that share an app. You choose the clients when you deploy, and each client's callback address comes from the catalogue that 'sf eca mcp clients' prints.
- Documentation link: https://developer.salesforce.com/docs/platform/hosted-mcp-servers/guide/create-external-client-app.html
- Tags: mcp, hosted-mcp, ai
- Parameter NAME: App API Name: API name for the External Client App in your org. When you do not give one, it is named after the client you choose, for example SalesforceMcpClaude.
- Parameter ADMIN_EMAIL: Administrator Contact Email: Email address of the person responsible for this app.
- Parameter MCP_CLIENTS: MCP Clients: The clients that sign in through this app, separated by commas, for example claude or claude,cursor. A client that needs a port is written claude-code:8123, and one that needs its own address is writt [...]
<!-- summary:end -->
