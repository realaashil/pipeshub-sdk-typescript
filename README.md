# pipeshub-sdk-typescript
<!-- Start Summary [summary] -->
## Summary

PipesHub API: Unified API documentation for PipesHub services.

PipesHub is an enterprise-grade platform providing:
- User authentication and management
- Document storage and version control
- Knowledge base management
- Enterprise search and conversational AI
- Third-party integrations via connectors
- System configuration management
- Crawling job scheduling
- Email services

## Authentication
Most endpoints require JWT Bearer token authentication. Some internal endpoints use scoped tokens for service-to-service communication.

## Base URLs
All endpoints use the `/api/v1` prefix unless otherwise noted.
<!-- End Summary [summary] -->

<!-- Start Table of Contents [toc] -->
## Table of Contents
<!-- $toc-max-depth=2 -->
* [pipeshub-sdk-typescirpt](#pipeshub-sdk-typescirpt)
  * [Authentication](#authentication)
  * [Base URLs](#base-urls)
  * [SDK Installation](#sdk-installation)
  * [Requirements](#requirements)
  * [SDK Example Usage](#sdk-example-usage)
  * [Authentication](#authentication-1)
  * [Available Resources and Operations](#available-resources-and-operations)
  * [Standalone functions](#standalone-functions)
  * [Server-sent event streaming](#server-sent-event-streaming)
  * [File uploads](#file-uploads)
  * [Retries](#retries)
  * [Error Handling](#error-handling)
  * [Custom HTTP Client](#custom-http-client)
  * [Debugging](#debugging)

<!-- End Table of Contents [toc] -->

<!-- Start SDK Installation [installation] -->
## SDK Installation

> [!TIP]
> To finish publishing your SDK to npm and others you must [run your first generation action](https://www.speakeasy.com/docs/github-setup#step-by-step-guide).


The SDK can be installed with either [npm](https://www.npmjs.com/), [pnpm](https://pnpm.io/), [bun](https://bun.sh/) or [yarn](https://classic.yarnpkg.com/en/) package managers.

### NPM

```bash
npm add <UNSET>
```

### PNPM

```bash
pnpm add <UNSET>
```

### Bun

```bash
bun add <UNSET>
```

### Yarn

```bash
yarn add <UNSET>
```

> [!NOTE]
> This package is published with CommonJS and ES Modules (ESM) support.
<!-- End SDK Installation [installation] -->

<!-- Start Requirements [requirements] -->
## Requirements

For supported JavaScript runtimes, please consult [RUNTIMES.md](RUNTIMES.md).
<!-- End Requirements [requirements] -->

<!-- Start SDK Example Usage [usage] -->
## SDK Example Usage

### Example

```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
});

async function run() {
  const result = await pipeshub.userAccount.initializeAuth({
    email: "user@example.com",
  });

  console.log(result);
}

run();

```
<!-- End SDK Example Usage [usage] -->

<!-- Start Authentication [security] -->
## Authentication

### Per-Client Security Schemes

This SDK supports the following security scheme globally:

| Name         | Type | Scheme      | Environment Variable   |
| ------------ | ---- | ----------- | ---------------------- |
| `bearerAuth` | http | HTTP Bearer | `PIPESHUB_BEARER_AUTH` |

To authenticate with the API the `bearerAuth` parameter must be set when initializing the SDK client instance. For example:
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.userAccount.initializeAuth({
    email: "user@example.com",
  });

  console.log(result);
}

run();

```

### Per-Operation Security Schemes

Some operations in this SDK require the security scheme to be specified at the request level. For example:
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
});

async function run() {
  const result = await pipeshub.userAccount.resetPasswordWithToken({
    scopedToken: process.env["PIPESHUB_SCOPED_TOKEN"] ?? "",
  }, {
    password: "H9GEHoL829GXj06",
  });

  console.log(result);
}

run();

```
<!-- End Authentication [security] -->

<!-- Start Available Resources and Operations [operations] -->
## Available Resources and Operations

<details open>
<summary>Available methods</summary>

### [AgentConversations](docs/sdks/agentconversations/README.md)

* [list](docs/sdks/agentconversations/README.md#list) - List agent conversations
* [start](docs/sdks/agentconversations/README.md#start) - Create agent conversation
* [stream](docs/sdks/agentconversations/README.md#stream) - Create agent conversation with streaming
* [get](docs/sdks/agentconversations/README.md#get) - Get agent conversation
* [delete](docs/sdks/agentconversations/README.md#delete) - Delete agent conversation
* [addMessage](docs/sdks/agentconversations/README.md#addmessage) - Add message to agent conversation
* [streamMessage](docs/sdks/agentconversations/README.md#streammessage) - Add message with streaming
* [regenerate](docs/sdks/agentconversations/README.md#regenerate) - Regenerate agent response

### [Agents](docs/sdks/agents/README.md)

* [list](docs/sdks/agents/README.md#list) - List agents
* [create](docs/sdks/agents/README.md#create) - Create agent
* [listTools](docs/sdks/agents/README.md#listtools) - List available tools
* [get](docs/sdks/agents/README.md#get) - Get agent
* [update](docs/sdks/agents/README.md#update) - Update agent
* [delete](docs/sdks/agents/README.md#delete) - Delete agent
* [getPermissions](docs/sdks/agents/README.md#getpermissions) - Get agent permissions
* [updatePermissions](docs/sdks/agents/README.md#updatepermissions) - Update agent permissions
* [share](docs/sdks/agents/README.md#share) - Share agent
* [unshare](docs/sdks/agents/README.md#unshare) - Revoke agent access

### [AgentTemplates](docs/sdks/agenttemplates/README.md)

* [list](docs/sdks/agenttemplates/README.md#list) - List agent templates
* [create](docs/sdks/agenttemplates/README.md#create) - Create agent template
* [get](docs/sdks/agenttemplates/README.md#get) - Get agent template
* [update](docs/sdks/agenttemplates/README.md#update) - Update agent template
* [delete](docs/sdks/agenttemplates/README.md#delete) - Delete agent template

### [AiModelsConfiguration](docs/sdks/aimodelsconfiguration/README.md)

* [create](docs/sdks/aimodelsconfiguration/README.md#create) - Bulk create AI models configuration
* [getAll](docs/sdks/aimodelsconfiguration/README.md#getall) - Get all AI models configuration

### [AiModelsProviders](docs/sdks/aimodelsproviders/README.md)

* [list](docs/sdks/aimodelsproviders/README.md#list) - Get all AI model providers
* [getByType](docs/sdks/aimodelsproviders/README.md#getbytype) - Get models by type
* [getAvailableModelsByType](docs/sdks/aimodelsproviders/README.md#getavailablemodelsbytype) - Get available models for selection
* [add](docs/sdks/aimodelsproviders/README.md#add) - Add new AI model provider
* [update](docs/sdks/aimodelsproviders/README.md#update) - Update AI model provider
* [delete](docs/sdks/aimodelsproviders/README.md#delete) - Delete AI model provider
* [setDefault](docs/sdks/aimodelsproviders/README.md#setdefault) - Set default AI model

### [AuthConfig](docs/sdks/authconfig/README.md)

* [getMicrosoft](docs/sdks/authconfig/README.md#getmicrosoft) - Get Microsoft authentication configuration

### [AuthenticationConfiguration](docs/sdks/authenticationconfiguration/README.md)

* [setAzureAdAuthConfig](docs/sdks/authenticationconfiguration/README.md#setazureadauthconfig) - Configure Azure AD authentication
* [getAzureAd](docs/sdks/authenticationconfiguration/README.md#getazuread) - Get Azure AD configuration
* [setGoogleAuthConfig](docs/sdks/authenticationconfiguration/README.md#setgoogleauthconfig) - Configure Google authentication
* [getGoogle](docs/sdks/authenticationconfiguration/README.md#getgoogle) - Get Google authentication configuration
* [setupSso](docs/sdks/authenticationconfiguration/README.md#setupsso) - Configure SAML SSO authentication
* [getSsoConfig](docs/sdks/authenticationconfiguration/README.md#getssoconfig) - Get SAML SSO configuration
* [setupOAuth](docs/sdks/authenticationconfiguration/README.md#setupoauth) - Configure generic OAuth provider
* [getOAuth](docs/sdks/authenticationconfiguration/README.md#getoauth) - Get generic OAuth configuration

### [AuthenticationConfigurations](docs/sdks/authenticationconfigurations/README.md)

* [configureMicrosoft](docs/sdks/authenticationconfigurations/README.md#configuremicrosoft) - Configure Microsoft authentication

### [Connector](docs/sdks/connector/README.md)

* [reindex](docs/sdks/connector/README.md#reindex) - Reindex single record
* [reindexRecordGroup](docs/sdks/connector/README.md#reindexrecordgroup) - Reindex record group
* [reindexFailed](docs/sdks/connector/README.md#reindexfailed) - Reindex failed connector records
* [resync](docs/sdks/connector/README.md#resync) - Resync connector
* [getStats](docs/sdks/connector/README.md#getstats) - Get connector statistics

### [ConnectorConfiguration](docs/sdks/connectorconfiguration/README.md)

* [get](docs/sdks/connectorconfiguration/README.md#get) - Get connector configuration
* [update](docs/sdks/connectorconfiguration/README.md#update) - Update connector configuration
* [updateFiltersSync](docs/sdks/connectorconfiguration/README.md#updatefilterssync) - Update filters and sync configuration

### [ConnectorConfigurations](docs/sdks/connectorconfigurations/README.md)

* [updateAuth](docs/sdks/connectorconfigurations/README.md#updateauth) - Update authentication configuration
* [getGoogleWorkspaceCredentials](docs/sdks/connectorconfigurations/README.md#getgoogleworkspacecredentials) - Get Google Workspace credentials status

### [ConnectorControl](docs/sdks/connectorcontrol/README.md)

* [toggle](docs/sdks/connectorcontrol/README.md#toggle) - Toggle connector sync or agent

### [ConnectorFilters](docs/sdks/connectorfilters/README.md)

* [getOptions](docs/sdks/connectorfilters/README.md#getoptions) - Get filter options
* [save](docs/sdks/connectorfilters/README.md#save) - Save filter selections
* [getFieldOptions](docs/sdks/connectorfilters/README.md#getfieldoptions) - Get dynamic filter options

### [ConnectorInstances](docs/sdks/connectorinstances/README.md)

* [list](docs/sdks/connectorinstances/README.md#list) - List connector instances
* [create](docs/sdks/connectorinstances/README.md#create) - Create connector instance
* [listActive](docs/sdks/connectorinstances/README.md#listactive) - List active connector instances
* [listInactive](docs/sdks/connectorinstances/README.md#listinactive) - List inactive connector instances
* [listConfigured](docs/sdks/connectorinstances/README.md#listconfigured) - List configured connector instances
* [getActiveAgents](docs/sdks/connectorinstances/README.md#getactiveagents) - List active agent connectors
* [get](docs/sdks/connectorinstances/README.md#get) - Get connector instance
* [delete](docs/sdks/connectorinstances/README.md#delete) - Delete connector instance
* [updateName](docs/sdks/connectorinstances/README.md#updatename) - Update connector instance name

### [ConnectorOAuth](docs/sdks/connectoroauth/README.md)

* [getTokenFromCode](docs/sdks/connectoroauth/README.md#gettokenfromcode) - Exchange authorization code for tokens (legacy)
* [getAuthorizationUrl](docs/sdks/connectoroauth/README.md#getauthorizationurl) - Get OAuth authorization URL
* [handleCallback](docs/sdks/connectoroauth/README.md#handlecallback) - OAuth callback handler

### [ConnectorOauthConfiguration](docs/sdks/connectoroauthconfiguration2/README.md)

* [getAtlassianConfig](docs/sdks/connectoroauthconfiguration2/README.md#getatlassianconfig) - Get Atlassian OAuth configuration
* [getOneDriveConfig](docs/sdks/connectoroauthconfiguration2/README.md#getonedriveconfig) - Get OneDrive configuration

### [ConnectorOAuthConfiguration](docs/sdks/connectoroauthconfiguration1/README.md)

* [createGoogleWorkspaceCredentials](docs/sdks/connectoroauthconfiguration1/README.md#creategoogleworkspacecredentials) - Upload Google Workspace credentials
* [getGoogleWorkspace](docs/sdks/connectoroauthconfiguration1/README.md#getgoogleworkspace) - Get Google Workspace OAuth configuration
* [setAtlassianConfig](docs/sdks/connectoroauthconfiguration1/README.md#setatlassianconfig) - Configure Atlassian OAuth
* [getSharePointConfig](docs/sdks/connectoroauthconfiguration1/README.md#getsharepointconfig) - Get SharePoint configuration

### [ConnectorOAuthConfigurations](docs/sdks/connectoroauthconfigurations/README.md)

* [setGoogleWorkspaceOauth](docs/sdks/connectoroauthconfigurations/README.md#setgoogleworkspaceoauth) - Configure Google Workspace OAuth
* [configureOneDrive](docs/sdks/connectoroauthconfigurations/README.md#configureonedrive) - Configure OneDrive connector
* [setSharePointConfig](docs/sdks/connectoroauthconfigurations/README.md#setsharepointconfig) - Configure SharePoint connector

### [ConnectorRegistry](docs/sdks/connectorregistry/README.md)

* [list](docs/sdks/connectorregistry/README.md#list) - List available connector types
* [getSchema](docs/sdks/connectorregistry/README.md#getschema) - Get connector configuration schema

### [ConnectorService](docs/sdks/connectorservice/README.md)

* [checkHealth](docs/sdks/connectorservice/README.md#checkhealth) - [Connector Service] Health check
* [postDrive](docs/sdks/connectorservice/README.md#postdrive) - [Connector Service] Google Drive webhook
* [internalStreamRecord](docs/sdks/connectorservice/README.md#internalstreamrecord) - [Connector Service] Internal stream record
* [convertRecordBuffer](docs/sdks/connectorservice/README.md#convertrecordbuffer) - [Connector Service] Convert record buffer
* [getStats](docs/sdks/connectorservice/README.md#getstats) - [Connector Service] Get connector statistics
* [getSignedUrl](docs/sdks/connectorservice/README.md#getsignedurl) - [Connector Service] Get signed URL for record

### [ConnectorServices](docs/sdks/connectorservices/README.md)

* [reindexFailedRecords](docs/sdks/connectorservices/README.md#reindexfailedrecords) - [Connector Service] Reindex all failed records

### [Conversations](docs/sdks/conversations/README.md)

* [create](docs/sdks/conversations/README.md#create) - Create a new AI conversation
* [stream](docs/sdks/conversations/README.md#stream) - Create conversation with streaming response
* [list](docs/sdks/conversations/README.md#list) - List all conversations
* [listArchived](docs/sdks/conversations/README.md#listarchived) - List archived conversations
* [get](docs/sdks/conversations/README.md#get) - Get conversation by ID
* [delete](docs/sdks/conversations/README.md#delete) - Delete conversation
* [addMessage](docs/sdks/conversations/README.md#addmessage) - Add message to conversation
* [addMessageStream](docs/sdks/conversations/README.md#addmessagestream) - Add message with streaming response
* [share](docs/sdks/conversations/README.md#share) - Share conversation with users
* [unshare](docs/sdks/conversations/README.md#unshare) - Revoke conversation access
* [updateTitle](docs/sdks/conversations/README.md#updatetitle) - Update conversation title
* [patchArchive](docs/sdks/conversations/README.md#patcharchive) - Archive conversation
* [unarchive](docs/sdks/conversations/README.md#unarchive) - Unarchive conversation
* [regenerateAnswer](docs/sdks/conversations/README.md#regenerateanswer) - Regenerate AI response
* [updateMessageFeedback](docs/sdks/conversations/README.md#updatemessagefeedback) - Submit feedback on AI response

### [CrawlingJobs](docs/sdks/crawlingjobs/README.md)

* [schedule](docs/sdks/crawlingjobs/README.md#schedule) - Schedule a crawling job
* [getStatus](docs/sdks/crawlingjobs/README.md#getstatus) - Get crawling job status
* [remove](docs/sdks/crawlingjobs/README.md#remove) - Remove a crawling job
* [pause](docs/sdks/crawlingjobs/README.md#pause) - Pause a crawling job
* [resume](docs/sdks/crawlingjobs/README.md#resume) - Resume a paused crawling job
* [list](docs/sdks/crawlingjobs/README.md#list) - Get all crawling job statuses
* [removeAll](docs/sdks/crawlingjobs/README.md#removeall) - Remove all crawling jobs

### [DoclingService](docs/sdks/doclingservice/README.md)

* [healthCheck](docs/sdks/doclingservice/README.md#healthcheck) - [Docling Service] Health check
* [processPdf](docs/sdks/doclingservice/README.md#processpdf) - [Docling Service] Process PDF document
* [parsePdf](docs/sdks/doclingservice/README.md#parsepdf) - [Docling Service] Parse PDF (Phase 1)
* [createBlocks](docs/sdks/doclingservice/README.md#createblocks) - [Docling Service] Create blocks from parse result (Phase 2)

### [DocumentBuffer](docs/sdks/documentbuffer/README.md)

* [get](docs/sdks/documentbuffer/README.md#get) - Get document buffer
* [update](docs/sdks/documentbuffer/README.md#update) - Update document buffer

### [DocumentManagement](docs/sdks/documentmanagement/README.md)

* [getById](docs/sdks/documentmanagement/README.md#getbyid) - Get document by ID
* [delete](docs/sdks/documentmanagement/README.md#delete) - Delete document
* [download](docs/sdks/documentmanagement/README.md#download) - Download document

### [DocumentUpload](docs/sdks/documentupload/README.md)

* [upload](docs/sdks/documentupload/README.md#upload) - Upload a new document
* [createPlaceholder](docs/sdks/documentupload/README.md#createplaceholder) - Create document placeholder
* [getDirectUploadUrl](docs/sdks/documentupload/README.md#getdirectuploadurl) - Get direct upload URL

### [EmailOperations](docs/sdks/emailoperations/README.md)

* [send](docs/sdks/emailoperations/README.md#send) - Send a transactional email

### [Folders](docs/sdks/folders/README.md)

* [create](docs/sdks/folders/README.md#create) - Create root folder
* [getContents](docs/sdks/folders/README.md#getcontents) - Get folder contents
* [update](docs/sdks/folders/README.md#update) - Update folder
* [delete](docs/sdks/folders/README.md#delete) - Delete folder
* [createSubfolder](docs/sdks/folders/README.md#createsubfolder) - Create subfolder

### [IndexingService](docs/sdks/indexingservice/README.md)

* [health](docs/sdks/indexingservice/README.md#health) - [Indexing Service] Health check

### [KnowledgeBases](docs/sdks/knowledgebases/README.md)

* [create](docs/sdks/knowledgebases/README.md#create) - Create a new knowledge base
* [list](docs/sdks/knowledgebases/README.md#list) - List all knowledge bases
* [get](docs/sdks/knowledgebases/README.md#get) - Get knowledge base by ID
* [update](docs/sdks/knowledgebases/README.md#update) - Update knowledge base
* [delete](docs/sdks/knowledgebases/README.md#delete) - Delete knowledge base
* [getRootNodes](docs/sdks/knowledgebases/README.md#getrootnodes) - Get knowledge hub root nodes
* [getHubChildNodes](docs/sdks/knowledgebases/README.md#gethubchildnodes) - Get knowledge hub child nodes

### [MailConfiguration](docs/sdks/mailconfiguration/README.md)

* [updateSmtp](docs/sdks/mailconfiguration/README.md#updatesmtp) - Reload SMTP configuration

### [MetricsCollection](docs/sdks/metricscollection/README.md)

* [getConfiguration](docs/sdks/metricscollection/README.md#getconfiguration) - Get metrics collection configuration
* [setPushInterval](docs/sdks/metricscollection/README.md#setpushinterval) - Configure metrics push interval
* [setServerUrl](docs/sdks/metricscollection/README.md#setserverurl) - Configure metrics server URL

### [MetricsCollections](docs/sdks/metricscollections/README.md)

* [toggle](docs/sdks/metricscollections/README.md#toggle) - Enable or disable metrics collection

### [Oauth](docs/sdks/oauth/README.md)

* [exchangeCode](docs/sdks/oauth/README.md#exchangecode) - Exchange OAuth authorization code for tokens

### [OauthApps](docs/sdks/oauthapps/README.md)

* [list](docs/sdks/oauthapps/README.md#list) - List OAuth apps
* [create](docs/sdks/oauthapps/README.md#create) - Create OAuth app
* [listScopes](docs/sdks/oauthapps/README.md#listscopes) - List available scopes
* [get](docs/sdks/oauthapps/README.md#get) - Get OAuth app details
* [update](docs/sdks/oauthapps/README.md#update) - Update OAuth app
* [delete](docs/sdks/oauthapps/README.md#delete) - Delete OAuth app
* [regenerateSecret](docs/sdks/oauthapps/README.md#regeneratesecret) - Regenerate client secret
* [suspend](docs/sdks/oauthapps/README.md#suspend) - Suspend OAuth app
* [activate](docs/sdks/oauthapps/README.md#activate) - Activate suspended OAuth app
* [listTokens](docs/sdks/oauthapps/README.md#listtokens) - List app tokens
* [revokeAllTokens](docs/sdks/oauthapps/README.md#revokealltokens) - Revoke all app tokens

### [OauthConfiguration](docs/sdks/oauthconfiguration1/README.md)

* [getRegistry](docs/sdks/oauthconfiguration1/README.md#getregistry) - List OAuth-capable connector types
* [list](docs/sdks/oauthconfiguration1/README.md#list) - List OAuth configurations
* [listConfigsByType](docs/sdks/oauthconfiguration1/README.md#listconfigsbytype) - List OAuth configs for connector type
* [get](docs/sdks/oauthconfiguration1/README.md#get) - Get OAuth configuration
* [update](docs/sdks/oauthconfiguration1/README.md#update) - Update OAuth configuration

### [OAuthConfiguration](docs/sdks/oauthconfiguration2/README.md)

* [create](docs/sdks/oauthconfiguration2/README.md#create) - Create OAuth configuration

### [OauthConfigurations](docs/sdks/oauthconfigurations/README.md)

* [getConnectorType](docs/sdks/oauthconfigurations/README.md#getconnectortype) - Get OAuth connector type details
* [deleteConfiguration](docs/sdks/oauthconfigurations/README.md#deleteconfiguration) - Delete OAuth configuration

### [OauthProvider](docs/sdks/oauthprovider/README.md)

* [authorize](docs/sdks/oauthprovider/README.md#authorize) - Initiate OAuth authorization flow
* [submitConsent](docs/sdks/oauthprovider/README.md#submitconsent) - Submit authorization consent
* [exchange](docs/sdks/oauthprovider/README.md#exchange) - Exchange authorization code for tokens
* [revokeToken](docs/sdks/oauthprovider/README.md#revoketoken) - Revoke an access or refresh token
* [introspect](docs/sdks/oauthprovider/README.md#introspect) - Introspect a token

### [OpenIDConnect](docs/sdks/openidconnect/README.md)

* [getUserInfo](docs/sdks/openidconnect/README.md#getuserinfo) - Get authenticated user information
* [getConfiguration](docs/sdks/openidconnect/README.md#getconfiguration) - OpenID Connect Discovery
* [jwks](docs/sdks/openidconnect/README.md#jwks) - JSON Web Key Set

### [OrganizationAuthConfig](docs/sdks/organizationauthconfig/README.md)

* [getAuthMethods](docs/sdks/organizationauthconfig/README.md#getauthmethods) - Get organization authentication methods

### [OrganizationAuthConfigs](docs/sdks/organizationauthconfigs/README.md)

* [create](docs/sdks/organizationauthconfigs/README.md#create) - Create organization authentication configuration

### [OrganizationAuthConfiguration](docs/sdks/organizationauthconfiguration/README.md)

* [updateMethod](docs/sdks/organizationauthconfiguration/README.md#updatemethod) - Update organization authentication methods

### [Organizations](docs/sdks/organizations/README.md)

* [checkExists](docs/sdks/organizations/README.md#checkexists) - Check if organization exists
* [create](docs/sdks/organizations/README.md#create) - Create organization
* [getCurrent](docs/sdks/organizations/README.md#getcurrent) - Get current organization
* [update](docs/sdks/organizations/README.md#update) - Update organization
* [delete](docs/sdks/organizations/README.md#delete) - Delete organization
* [uploadLogo](docs/sdks/organizations/README.md#uploadlogo) - Upload organization logo
* [getLogo](docs/sdks/organizations/README.md#getlogo) - Get organization logo
* [deleteLogo](docs/sdks/organizations/README.md#deletelogo) - Delete organization logo
* [getOnboardingStatus](docs/sdks/organizations/README.md#getonboardingstatus) - Get onboarding status
* [updateOnboardingStatus](docs/sdks/organizations/README.md#updateonboardingstatus) - Update onboarding status

### [Permissions](docs/sdks/permissions/README.md)

* [grant](docs/sdks/permissions/README.md#grant) - Grant permissions
* [list](docs/sdks/permissions/README.md#list) - List permissions
* [update](docs/sdks/permissions/README.md#update) - Update permissions
* [remove](docs/sdks/permissions/README.md#remove) - Remove permissions

### [PlatformSettings](docs/sdks/platformsettings/README.md)

* [update](docs/sdks/platformsettings/README.md#update) - Update platform settings
* [get](docs/sdks/platformsettings/README.md#get) - Get platform settings
* [getFeatureFlags](docs/sdks/platformsettings/README.md#getfeatureflags) - Get available feature flags
* [updateSystemPrompt](docs/sdks/platformsettings/README.md#updatesystemprompt) - Update custom system prompt
* [getCustomSystemPrompt](docs/sdks/platformsettings/README.md#getcustomsystemprompt) - Get custom system prompt

### [PublicUrls](docs/sdks/publicurls/README.md)

* [setFrontendUrl](docs/sdks/publicurls/README.md#setfrontendurl) - Set frontend public URL
* [getFrontend](docs/sdks/publicurls/README.md#getfrontend) - Get frontend public URL
* [setConnector](docs/sdks/publicurls/README.md#setconnector) - Set connector public URL
* [getConnector](docs/sdks/publicurls/README.md#getconnector) - Get connector public URL

### [QueryService](docs/sdks/queryservice/README.md)

* [search](docs/sdks/queryservice/README.md#search) - [Query Service] Semantic search
* [chat](docs/sdks/queryservice/README.md#chat) - [Query Service] Chat with knowledge base
* [chatStream](docs/sdks/queryservice/README.md#chatstream) - [Query Service] Streaming chat with knowledge base
* [healthCheck](docs/sdks/queryservice/README.md#healthcheck) - [Query Service] AI model health check
* [listTools](docs/sdks/queryservice/README.md#listtools) - [Query Service] List available agent tools

### [QueryServices](docs/sdks/queryservices/README.md)

* [getHealth](docs/sdks/queryservices/README.md#gethealth) - [Query Service] Health check

### [QueueManagement](docs/sdks/queuemanagement/README.md)

* [getStats](docs/sdks/queuemanagement/README.md#getstats) - Get queue statistics

### [Records](docs/sdks/records/README.md)

* [get](docs/sdks/records/README.md#get) - Get all records across knowledge bases
* [list](docs/sdks/records/README.md#list) - Get records for a knowledge base
* [getById](docs/sdks/records/README.md#getbyid) - Get record by ID
* [update](docs/sdks/records/README.md#update) - Update record
* [delete](docs/sdks/records/README.md#delete) - Delete record
* [streamContent](docs/sdks/records/README.md#streamcontent) - Stream record content
* [move](docs/sdks/records/README.md#move) - Move a record to another folder

### [Saml](docs/sdks/saml/README.md)

* [signIn](docs/sdks/saml/README.md#signin) - Initiate SAML sign-in flow
* [callback](docs/sdks/saml/README.md#callback) - SAML authentication callback
* [updateAppConfig](docs/sdks/saml/README.md#updateappconfig) - Reload SAML application configuration (Internal)

### [SemanticSearch](docs/sdks/semanticsearch/README.md)

* [postSearch](docs/sdks/semanticsearch/README.md#postsearch) - Perform semantic search
* [getHistory](docs/sdks/semanticsearch/README.md#gethistory) - Get search history
* [deleteAllHistory](docs/sdks/semanticsearch/README.md#deleteallhistory) - Clear all search history
* [getById](docs/sdks/semanticsearch/README.md#getbyid) - Get search by ID
* [delete](docs/sdks/semanticsearch/README.md#delete) - Delete search
* [patchShare](docs/sdks/semanticsearch/README.md#patchshare) - Share search results
* [unshare](docs/sdks/semanticsearch/README.md#unshare) - Revoke search access
* [archive](docs/sdks/semanticsearch/README.md#archive) - Archive search
* [unarchive](docs/sdks/semanticsearch/README.md#unarchive) - Unarchive search

### [SmtpConfiguration](docs/sdks/smtpconfiguration/README.md)

* [createOrUpdate](docs/sdks/smtpconfiguration/README.md#createorupdate) - Create or update SMTP configuration
* [get](docs/sdks/smtpconfiguration/README.md#get) - Get SMTP configuration

### [StorageConfiguration](docs/sdks/storageconfiguration/README.md)

* [configureLocal](docs/sdks/storageconfiguration/README.md#configurelocal) - Configure Local Storage
* [createS3StorageConfig](docs/sdks/storageconfiguration/README.md#creates3storageconfig) - Configure AWS S3 Storage
* [createAzureBlob](docs/sdks/storageconfiguration/README.md#createazureblob) - Configure Azure Blob Storage
* [get](docs/sdks/storageconfiguration/README.md#get) - Get current storage configuration

### [Teams](docs/sdks/teams/README.md)

* [create](docs/sdks/teams/README.md#create) - Create a team
* [list](docs/sdks/teams/README.md#list) - List teams
* [get](docs/sdks/teams/README.md#get) - Get team by ID
* [update](docs/sdks/teams/README.md#update) - Update team
* [delete](docs/sdks/teams/README.md#delete) - Delete team
* [getUsers](docs/sdks/teams/README.md#getusers) - Get team members
* [addUsers](docs/sdks/teams/README.md#addusers) - Add users to team
* [removeUsers](docs/sdks/teams/README.md#removeusers) - Remove users from team
* [updatePermissions](docs/sdks/teams/README.md#updatepermissions) - Update user role in team
* [getUser](docs/sdks/teams/README.md#getuser) - Get current user's teams
* [getCreatedByUser](docs/sdks/teams/README.md#getcreatedbyuser) - Get teams created by current user

### [Upload](docs/sdks/upload/README.md)

* [files](docs/sdks/upload/README.md#files) - Upload files to knowledge base
* [toFolder](docs/sdks/upload/README.md#tofolder) - Upload files to folder
* [getLimits](docs/sdks/upload/README.md#getlimits) - Get upload limits

### [UserAccount](docs/sdks/useraccount/README.md)

* [initializeAuth](docs/sdks/useraccount/README.md#initializeauth) - Initialize authentication session
* [authenticate](docs/sdks/useraccount/README.md#authenticate) - Authenticate user with credentials
* [generateLoginOtp](docs/sdks/useraccount/README.md#generateloginotp) - Generate and send OTP for login
* [resetPassword](docs/sdks/useraccount/README.md#resetpassword) - Reset password (authenticated user)
* [forgotPassword](docs/sdks/useraccount/README.md#forgotpassword) - Request password reset email
* [resetPasswordWithToken](docs/sdks/useraccount/README.md#resetpasswordwithtoken) - Reset password with email token
* [checkPasswordStatus](docs/sdks/useraccount/README.md#checkpasswordstatus) - Check if user has password set (Internal)
* [refresh](docs/sdks/useraccount/README.md#refresh) - Refresh access token
* [logout](docs/sdks/useraccount/README.md#logout) - Logout current session

### [UserGroups](docs/sdks/usergroups/README.md)

* [create](docs/sdks/usergroups/README.md#create) - Create user group
* [list](docs/sdks/usergroups/README.md#list) - Get all user groups
* [getById](docs/sdks/usergroups/README.md#getbyid) - Get user group by ID
* [update](docs/sdks/usergroups/README.md#update) - Update user group
* [delete](docs/sdks/usergroups/README.md#delete) - Delete user group
* [addUsers](docs/sdks/usergroups/README.md#addusers) - Add users to group
* [removeUsers](docs/sdks/usergroups/README.md#removeusers) - Remove users from group
* [getUsers](docs/sdks/usergroups/README.md#getusers) - Get users in a group
* [getUserGroups](docs/sdks/usergroups/README.md#getusergroups) - Get groups for a user
* [getStats](docs/sdks/usergroups/README.md#getstats) - Get user group statistics

### [Users](docs/sdks/users/README.md)

* [get](docs/sdks/users/README.md#get) - Get all users
* [create](docs/sdks/users/README.md#create) - Create a new user
* [getById](docs/sdks/users/README.md#getbyid) - Get user by ID
* [update](docs/sdks/users/README.md#update) - Update user
* [delete](docs/sdks/users/README.md#delete) - Delete user
* [fetchWithGroups](docs/sdks/users/README.md#fetchwithgroups) - Get all users with their groups
* [getEmail](docs/sdks/users/README.md#getemail) - Get user email by ID
* [getByIds](docs/sdks/users/README.md#getbyids) - Get users by IDs (bulk)
* [checkExistsByEmail](docs/sdks/users/README.md#checkexistsbyemail) - Check if user exists by email
* [getInternal](docs/sdks/users/README.md#getinternal) - Get user (internal service-to-service)
* [updateFullName](docs/sdks/users/README.md#updatefullname) - Update user full name
* [updateFirstName](docs/sdks/users/README.md#updatefirstname) - Update user first name
* [updateLastName](docs/sdks/users/README.md#updatelastname) - Update user last name
* [updateDesignation](docs/sdks/users/README.md#updatedesignation) - Update user designation
* [checkIsAdmin](docs/sdks/users/README.md#checkisadmin) - Check if user is admin
* [uploadDisplayPicture](docs/sdks/users/README.md#uploaddisplaypicture) - Upload display picture
* [getDisplayPicture](docs/sdks/users/README.md#getdisplaypicture) - Get display picture
* [removeDisplayPicture](docs/sdks/users/README.md#removedisplaypicture) - Remove display picture
* [bulkInvite](docs/sdks/users/README.md#bulkinvite) - Bulk invite users
* [resendInvite](docs/sdks/users/README.md#resendinvite) - Resend user invite
* [listGraph](docs/sdks/users/README.md#listgraph) - List users (paginated with graph data)
* [listTeams](docs/sdks/users/README.md#listteams) - Get current user's teams

### [VersionControl](docs/sdks/versioncontrol/README.md)

* [uploadNext](docs/sdks/versioncontrol/README.md#uploadnext) - Upload next version
* [rollBack](docs/sdks/versioncontrol/README.md#rollback) - Rollback to previous version
* [checkModified](docs/sdks/versioncontrol/README.md#checkmodified) - Check if document is modified

### [Webhooks](docs/sdks/webhooks/README.md)

* [verifyGmail](docs/sdks/webhooks/README.md#verifygmail) - [Connector Service] Gmail webhook verification
* [postGmail](docs/sdks/webhooks/README.md#postgmail) - [Connector Service] Gmail webhook
* [handle](docs/sdks/webhooks/README.md#handle) - [Connector Service] Google Workspace Admin webhook

</details>
<!-- End Available Resources and Operations [operations] -->

<!-- Start Standalone functions [standalone-funcs] -->
## Standalone functions

All the methods listed above are available as standalone functions. These
functions are ideal for use in applications running in the browser, serverless
runtimes or other environments where application bundle size is a primary
concern. When using a bundler to build your application, all unused
functionality will be either excluded from the final bundle or tree-shaken away.

To read more about standalone functions, check [FUNCTIONS.md](./FUNCTIONS.md).

<details>

<summary>Available standalone functions</summary>

- [`agentConversationsAddMessage`](docs/sdks/agentconversations/README.md#addmessage) - Add message to agent conversation
- [`agentConversationsDelete`](docs/sdks/agentconversations/README.md#delete) - Delete agent conversation
- [`agentConversationsGet`](docs/sdks/agentconversations/README.md#get) - Get agent conversation
- [`agentConversationsList`](docs/sdks/agentconversations/README.md#list) - List agent conversations
- [`agentConversationsRegenerate`](docs/sdks/agentconversations/README.md#regenerate) - Regenerate agent response
- [`agentConversationsStart`](docs/sdks/agentconversations/README.md#start) - Create agent conversation
- [`agentConversationsStream`](docs/sdks/agentconversations/README.md#stream) - Create agent conversation with streaming
- [`agentConversationsStreamMessage`](docs/sdks/agentconversations/README.md#streammessage) - Add message with streaming
- [`agentsCreate`](docs/sdks/agents/README.md#create) - Create agent
- [`agentsDelete`](docs/sdks/agents/README.md#delete) - Delete agent
- [`agentsGet`](docs/sdks/agents/README.md#get) - Get agent
- [`agentsGetPermissions`](docs/sdks/agents/README.md#getpermissions) - Get agent permissions
- [`agentsList`](docs/sdks/agents/README.md#list) - List agents
- [`agentsListTools`](docs/sdks/agents/README.md#listtools) - List available tools
- [`agentsShare`](docs/sdks/agents/README.md#share) - Share agent
- [`agentsUnshare`](docs/sdks/agents/README.md#unshare) - Revoke agent access
- [`agentsUpdate`](docs/sdks/agents/README.md#update) - Update agent
- [`agentsUpdatePermissions`](docs/sdks/agents/README.md#updatepermissions) - Update agent permissions
- [`agentTemplatesCreate`](docs/sdks/agenttemplates/README.md#create) - Create agent template
- [`agentTemplatesDelete`](docs/sdks/agenttemplates/README.md#delete) - Delete agent template
- [`agentTemplatesGet`](docs/sdks/agenttemplates/README.md#get) - Get agent template
- [`agentTemplatesList`](docs/sdks/agenttemplates/README.md#list) - List agent templates
- [`agentTemplatesUpdate`](docs/sdks/agenttemplates/README.md#update) - Update agent template
- [`aiModelsConfigurationCreate`](docs/sdks/aimodelsconfiguration/README.md#create) - Bulk create AI models configuration
- [`aiModelsConfigurationGetAll`](docs/sdks/aimodelsconfiguration/README.md#getall) - Get all AI models configuration
- [`aiModelsProvidersAdd`](docs/sdks/aimodelsproviders/README.md#add) - Add new AI model provider
- [`aiModelsProvidersDelete`](docs/sdks/aimodelsproviders/README.md#delete) - Delete AI model provider
- [`aiModelsProvidersGetAvailableModelsByType`](docs/sdks/aimodelsproviders/README.md#getavailablemodelsbytype) - Get available models for selection
- [`aiModelsProvidersGetByType`](docs/sdks/aimodelsproviders/README.md#getbytype) - Get models by type
- [`aiModelsProvidersList`](docs/sdks/aimodelsproviders/README.md#list) - Get all AI model providers
- [`aiModelsProvidersSetDefault`](docs/sdks/aimodelsproviders/README.md#setdefault) - Set default AI model
- [`aiModelsProvidersUpdate`](docs/sdks/aimodelsproviders/README.md#update) - Update AI model provider
- [`authConfigGetMicrosoft`](docs/sdks/authconfig/README.md#getmicrosoft) - Get Microsoft authentication configuration
- [`authenticationConfigurationGetAzureAd`](docs/sdks/authenticationconfiguration/README.md#getazuread) - Get Azure AD configuration
- [`authenticationConfigurationGetGoogle`](docs/sdks/authenticationconfiguration/README.md#getgoogle) - Get Google authentication configuration
- [`authenticationConfigurationGetOAuth`](docs/sdks/authenticationconfiguration/README.md#getoauth) - Get generic OAuth configuration
- [`authenticationConfigurationGetSsoConfig`](docs/sdks/authenticationconfiguration/README.md#getssoconfig) - Get SAML SSO configuration
- [`authenticationConfigurationsConfigureMicrosoft`](docs/sdks/authenticationconfigurations/README.md#configuremicrosoft) - Configure Microsoft authentication
- [`authenticationConfigurationSetAzureAdAuthConfig`](docs/sdks/authenticationconfiguration/README.md#setazureadauthconfig) - Configure Azure AD authentication
- [`authenticationConfigurationSetGoogleAuthConfig`](docs/sdks/authenticationconfiguration/README.md#setgoogleauthconfig) - Configure Google authentication
- [`authenticationConfigurationSetupOAuth`](docs/sdks/authenticationconfiguration/README.md#setupoauth) - Configure generic OAuth provider
- [`authenticationConfigurationSetupSso`](docs/sdks/authenticationconfiguration/README.md#setupsso) - Configure SAML SSO authentication
- [`connectorConfigurationGet`](docs/sdks/connectorconfiguration/README.md#get) - Get connector configuration
- [`connectorConfigurationsGetGoogleWorkspaceCredentials`](docs/sdks/connectorconfigurations/README.md#getgoogleworkspacecredentials) - Get Google Workspace credentials status
- [`connectorConfigurationsUpdateAuth`](docs/sdks/connectorconfigurations/README.md#updateauth) - Update authentication configuration
- [`connectorConfigurationUpdate`](docs/sdks/connectorconfiguration/README.md#update) - Update connector configuration
- [`connectorConfigurationUpdateFiltersSync`](docs/sdks/connectorconfiguration/README.md#updatefilterssync) - Update filters and sync configuration
- [`connectorControlToggle`](docs/sdks/connectorcontrol/README.md#toggle) - Toggle connector sync or agent
- [`connectorFiltersGetFieldOptions`](docs/sdks/connectorfilters/README.md#getfieldoptions) - Get dynamic filter options
- [`connectorFiltersGetOptions`](docs/sdks/connectorfilters/README.md#getoptions) - Get filter options
- [`connectorFiltersSave`](docs/sdks/connectorfilters/README.md#save) - Save filter selections
- [`connectorGetStats`](docs/sdks/connector/README.md#getstats) - Get connector statistics
- [`connectorInstancesCreate`](docs/sdks/connectorinstances/README.md#create) - Create connector instance
- [`connectorInstancesDelete`](docs/sdks/connectorinstances/README.md#delete) - Delete connector instance
- [`connectorInstancesGet`](docs/sdks/connectorinstances/README.md#get) - Get connector instance
- [`connectorInstancesGetActiveAgents`](docs/sdks/connectorinstances/README.md#getactiveagents) - List active agent connectors
- [`connectorInstancesList`](docs/sdks/connectorinstances/README.md#list) - List connector instances
- [`connectorInstancesListActive`](docs/sdks/connectorinstances/README.md#listactive) - List active connector instances
- [`connectorInstancesListConfigured`](docs/sdks/connectorinstances/README.md#listconfigured) - List configured connector instances
- [`connectorInstancesListInactive`](docs/sdks/connectorinstances/README.md#listinactive) - List inactive connector instances
- [`connectorInstancesUpdateName`](docs/sdks/connectorinstances/README.md#updatename) - Update connector instance name
- [`connectorOAuthConfigurationCreateGoogleWorkspaceCredentials`](docs/sdks/connectoroauthconfiguration1/README.md#creategoogleworkspacecredentials) - Upload Google Workspace credentials
- [`connectorOauthConfigurationGetAtlassianConfig`](docs/sdks/connectoroauthconfiguration2/README.md#getatlassianconfig) - Get Atlassian OAuth configuration
- [`connectorOAuthConfigurationGetGoogleWorkspace`](docs/sdks/connectoroauthconfiguration1/README.md#getgoogleworkspace) - Get Google Workspace OAuth configuration
- [`connectorOauthConfigurationGetOneDriveConfig`](docs/sdks/connectoroauthconfiguration2/README.md#getonedriveconfig) - Get OneDrive configuration
- [`connectorOAuthConfigurationGetSharePointConfig`](docs/sdks/connectoroauthconfiguration1/README.md#getsharepointconfig) - Get SharePoint configuration
- [`connectorOAuthConfigurationsConfigureOneDrive`](docs/sdks/connectoroauthconfigurations/README.md#configureonedrive) - Configure OneDrive connector
- [`connectorOAuthConfigurationSetAtlassianConfig`](docs/sdks/connectoroauthconfiguration1/README.md#setatlassianconfig) - Configure Atlassian OAuth
- [`connectorOAuthConfigurationsSetGoogleWorkspaceOauth`](docs/sdks/connectoroauthconfigurations/README.md#setgoogleworkspaceoauth) - Configure Google Workspace OAuth
- [`connectorOAuthConfigurationsSetSharePointConfig`](docs/sdks/connectoroauthconfigurations/README.md#setsharepointconfig) - Configure SharePoint connector
- [`connectorOAuthGetAuthorizationUrl`](docs/sdks/connectoroauth/README.md#getauthorizationurl) - Get OAuth authorization URL
- [`connectorOAuthGetTokenFromCode`](docs/sdks/connectoroauth/README.md#gettokenfromcode) - Exchange authorization code for tokens (legacy)
- [`connectorOAuthHandleCallback`](docs/sdks/connectoroauth/README.md#handlecallback) - OAuth callback handler
- [`connectorRegistryGetSchema`](docs/sdks/connectorregistry/README.md#getschema) - Get connector configuration schema
- [`connectorRegistryList`](docs/sdks/connectorregistry/README.md#list) - List available connector types
- [`connectorReindex`](docs/sdks/connector/README.md#reindex) - Reindex single record
- [`connectorReindexFailed`](docs/sdks/connector/README.md#reindexfailed) - Reindex failed connector records
- [`connectorReindexRecordGroup`](docs/sdks/connector/README.md#reindexrecordgroup) - Reindex record group
- [`connectorResync`](docs/sdks/connector/README.md#resync) - Resync connector
- [`connectorServiceCheckHealth`](docs/sdks/connectorservice/README.md#checkhealth) - [Connector Service] Health check
- [`connectorServiceConvertRecordBuffer`](docs/sdks/connectorservice/README.md#convertrecordbuffer) - [Connector Service] Convert record buffer
- [`connectorServiceGetSignedUrl`](docs/sdks/connectorservice/README.md#getsignedurl) - [Connector Service] Get signed URL for record
- [`connectorServiceGetStats`](docs/sdks/connectorservice/README.md#getstats) - [Connector Service] Get connector statistics
- [`connectorServiceInternalStreamRecord`](docs/sdks/connectorservice/README.md#internalstreamrecord) - [Connector Service] Internal stream record
- [`connectorServicePostDrive`](docs/sdks/connectorservice/README.md#postdrive) - [Connector Service] Google Drive webhook
- [`connectorServicesReindexFailedRecords`](docs/sdks/connectorservices/README.md#reindexfailedrecords) - [Connector Service] Reindex all failed records
- [`conversationsAddMessage`](docs/sdks/conversations/README.md#addmessage) - Add message to conversation
- [`conversationsAddMessageStream`](docs/sdks/conversations/README.md#addmessagestream) - Add message with streaming response
- [`conversationsCreate`](docs/sdks/conversations/README.md#create) - Create a new AI conversation
- [`conversationsDelete`](docs/sdks/conversations/README.md#delete) - Delete conversation
- [`conversationsGet`](docs/sdks/conversations/README.md#get) - Get conversation by ID
- [`conversationsList`](docs/sdks/conversations/README.md#list) - List all conversations
- [`conversationsListArchived`](docs/sdks/conversations/README.md#listarchived) - List archived conversations
- [`conversationsPatchArchive`](docs/sdks/conversations/README.md#patcharchive) - Archive conversation
- [`conversationsRegenerateAnswer`](docs/sdks/conversations/README.md#regenerateanswer) - Regenerate AI response
- [`conversationsShare`](docs/sdks/conversations/README.md#share) - Share conversation with users
- [`conversationsStream`](docs/sdks/conversations/README.md#stream) - Create conversation with streaming response
- [`conversationsUnarchive`](docs/sdks/conversations/README.md#unarchive) - Unarchive conversation
- [`conversationsUnshare`](docs/sdks/conversations/README.md#unshare) - Revoke conversation access
- [`conversationsUpdateMessageFeedback`](docs/sdks/conversations/README.md#updatemessagefeedback) - Submit feedback on AI response
- [`conversationsUpdateTitle`](docs/sdks/conversations/README.md#updatetitle) - Update conversation title
- [`crawlingJobsGetStatus`](docs/sdks/crawlingjobs/README.md#getstatus) - Get crawling job status
- [`crawlingJobsList`](docs/sdks/crawlingjobs/README.md#list) - Get all crawling job statuses
- [`crawlingJobsPause`](docs/sdks/crawlingjobs/README.md#pause) - Pause a crawling job
- [`crawlingJobsRemove`](docs/sdks/crawlingjobs/README.md#remove) - Remove a crawling job
- [`crawlingJobsRemoveAll`](docs/sdks/crawlingjobs/README.md#removeall) - Remove all crawling jobs
- [`crawlingJobsResume`](docs/sdks/crawlingjobs/README.md#resume) - Resume a paused crawling job
- [`crawlingJobsSchedule`](docs/sdks/crawlingjobs/README.md#schedule) - Schedule a crawling job
- [`doclingServiceCreateBlocks`](docs/sdks/doclingservice/README.md#createblocks) - [Docling Service] Create blocks from parse result (Phase 2)
- [`doclingServiceHealthCheck`](docs/sdks/doclingservice/README.md#healthcheck) - [Docling Service] Health check
- [`doclingServiceParsePdf`](docs/sdks/doclingservice/README.md#parsepdf) - [Docling Service] Parse PDF (Phase 1)
- [`doclingServiceProcessPdf`](docs/sdks/doclingservice/README.md#processpdf) - [Docling Service] Process PDF document
- [`documentBufferGet`](docs/sdks/documentbuffer/README.md#get) - Get document buffer
- [`documentBufferUpdate`](docs/sdks/documentbuffer/README.md#update) - Update document buffer
- [`documentManagementDelete`](docs/sdks/documentmanagement/README.md#delete) - Delete document
- [`documentManagementDownload`](docs/sdks/documentmanagement/README.md#download) - Download document
- [`documentManagementGetById`](docs/sdks/documentmanagement/README.md#getbyid) - Get document by ID
- [`documentUploadCreatePlaceholder`](docs/sdks/documentupload/README.md#createplaceholder) - Create document placeholder
- [`documentUploadGetDirectUploadUrl`](docs/sdks/documentupload/README.md#getdirectuploadurl) - Get direct upload URL
- [`documentUploadUpload`](docs/sdks/documentupload/README.md#upload) - Upload a new document
- [`emailOperationsSend`](docs/sdks/emailoperations/README.md#send) - Send a transactional email
- [`foldersCreate`](docs/sdks/folders/README.md#create) - Create root folder
- [`foldersCreateSubfolder`](docs/sdks/folders/README.md#createsubfolder) - Create subfolder
- [`foldersDelete`](docs/sdks/folders/README.md#delete) - Delete folder
- [`foldersGetContents`](docs/sdks/folders/README.md#getcontents) - Get folder contents
- [`foldersUpdate`](docs/sdks/folders/README.md#update) - Update folder
- [`indexingServiceHealth`](docs/sdks/indexingservice/README.md#health) - [Indexing Service] Health check
- [`knowledgeBasesCreate`](docs/sdks/knowledgebases/README.md#create) - Create a new knowledge base
- [`knowledgeBasesDelete`](docs/sdks/knowledgebases/README.md#delete) - Delete knowledge base
- [`knowledgeBasesGet`](docs/sdks/knowledgebases/README.md#get) - Get knowledge base by ID
- [`knowledgeBasesGetHubChildNodes`](docs/sdks/knowledgebases/README.md#gethubchildnodes) - Get knowledge hub child nodes
- [`knowledgeBasesGetRootNodes`](docs/sdks/knowledgebases/README.md#getrootnodes) - Get knowledge hub root nodes
- [`knowledgeBasesList`](docs/sdks/knowledgebases/README.md#list) - List all knowledge bases
- [`knowledgeBasesUpdate`](docs/sdks/knowledgebases/README.md#update) - Update knowledge base
- [`mailConfigurationUpdateSmtp`](docs/sdks/mailconfiguration/README.md#updatesmtp) - Reload SMTP configuration
- [`metricsCollectionGetConfiguration`](docs/sdks/metricscollection/README.md#getconfiguration) - Get metrics collection configuration
- [`metricsCollectionSetPushInterval`](docs/sdks/metricscollection/README.md#setpushinterval) - Configure metrics push interval
- [`metricsCollectionSetServerUrl`](docs/sdks/metricscollection/README.md#setserverurl) - Configure metrics server URL
- [`metricsCollectionsToggle`](docs/sdks/metricscollections/README.md#toggle) - Enable or disable metrics collection
- [`oauthAppsActivate`](docs/sdks/oauthapps/README.md#activate) - Activate suspended OAuth app
- [`oauthAppsCreate`](docs/sdks/oauthapps/README.md#create) - Create OAuth app
- [`oauthAppsDelete`](docs/sdks/oauthapps/README.md#delete) - Delete OAuth app
- [`oauthAppsGet`](docs/sdks/oauthapps/README.md#get) - Get OAuth app details
- [`oauthAppsList`](docs/sdks/oauthapps/README.md#list) - List OAuth apps
- [`oauthAppsListScopes`](docs/sdks/oauthapps/README.md#listscopes) - List available scopes
- [`oauthAppsListTokens`](docs/sdks/oauthapps/README.md#listtokens) - List app tokens
- [`oauthAppsRegenerateSecret`](docs/sdks/oauthapps/README.md#regeneratesecret) - Regenerate client secret
- [`oauthAppsRevokeAllTokens`](docs/sdks/oauthapps/README.md#revokealltokens) - Revoke all app tokens
- [`oauthAppsSuspend`](docs/sdks/oauthapps/README.md#suspend) - Suspend OAuth app
- [`oauthAppsUpdate`](docs/sdks/oauthapps/README.md#update) - Update OAuth app
- [`oAuthConfigurationCreate`](docs/sdks/oauthconfiguration2/README.md#create) - Create OAuth configuration
- [`oauthConfigurationGet`](docs/sdks/oauthconfiguration1/README.md#get) - Get OAuth configuration
- [`oauthConfigurationGetRegistry`](docs/sdks/oauthconfiguration1/README.md#getregistry) - List OAuth-capable connector types
- [`oauthConfigurationList`](docs/sdks/oauthconfiguration1/README.md#list) - List OAuth configurations
- [`oauthConfigurationListConfigsByType`](docs/sdks/oauthconfiguration1/README.md#listconfigsbytype) - List OAuth configs for connector type
- [`oauthConfigurationsDeleteConfiguration`](docs/sdks/oauthconfigurations/README.md#deleteconfiguration) - Delete OAuth configuration
- [`oauthConfigurationsGetConnectorType`](docs/sdks/oauthconfigurations/README.md#getconnectortype) - Get OAuth connector type details
- [`oauthConfigurationUpdate`](docs/sdks/oauthconfiguration1/README.md#update) - Update OAuth configuration
- [`oauthExchangeCode`](docs/sdks/oauth/README.md#exchangecode) - Exchange OAuth authorization code for tokens
- [`oauthProviderAuthorize`](docs/sdks/oauthprovider/README.md#authorize) - Initiate OAuth authorization flow
- [`oauthProviderExchange`](docs/sdks/oauthprovider/README.md#exchange) - Exchange authorization code for tokens
- [`oauthProviderIntrospect`](docs/sdks/oauthprovider/README.md#introspect) - Introspect a token
- [`oauthProviderRevokeToken`](docs/sdks/oauthprovider/README.md#revoketoken) - Revoke an access or refresh token
- [`oauthProviderSubmitConsent`](docs/sdks/oauthprovider/README.md#submitconsent) - Submit authorization consent
- [`openIDConnectGetConfiguration`](docs/sdks/openidconnect/README.md#getconfiguration) - OpenID Connect Discovery
- [`openIDConnectGetUserInfo`](docs/sdks/openidconnect/README.md#getuserinfo) - Get authenticated user information
- [`openIDConnectJwks`](docs/sdks/openidconnect/README.md#jwks) - JSON Web Key Set
- [`organizationAuthConfigGetAuthMethods`](docs/sdks/organizationauthconfig/README.md#getauthmethods) - Get organization authentication methods
- [`organizationAuthConfigsCreate`](docs/sdks/organizationauthconfigs/README.md#create) - Create organization authentication configuration
- [`organizationAuthConfigurationUpdateMethod`](docs/sdks/organizationauthconfiguration/README.md#updatemethod) - Update organization authentication methods
- [`organizationsCheckExists`](docs/sdks/organizations/README.md#checkexists) - Check if organization exists
- [`organizationsCreate`](docs/sdks/organizations/README.md#create) - Create organization
- [`organizationsDelete`](docs/sdks/organizations/README.md#delete) - Delete organization
- [`organizationsDeleteLogo`](docs/sdks/organizations/README.md#deletelogo) - Delete organization logo
- [`organizationsGetCurrent`](docs/sdks/organizations/README.md#getcurrent) - Get current organization
- [`organizationsGetLogo`](docs/sdks/organizations/README.md#getlogo) - Get organization logo
- [`organizationsGetOnboardingStatus`](docs/sdks/organizations/README.md#getonboardingstatus) - Get onboarding status
- [`organizationsUpdate`](docs/sdks/organizations/README.md#update) - Update organization
- [`organizationsUpdateOnboardingStatus`](docs/sdks/organizations/README.md#updateonboardingstatus) - Update onboarding status
- [`organizationsUploadLogo`](docs/sdks/organizations/README.md#uploadlogo) - Upload organization logo
- [`permissionsGrant`](docs/sdks/permissions/README.md#grant) - Grant permissions
- [`permissionsList`](docs/sdks/permissions/README.md#list) - List permissions
- [`permissionsRemove`](docs/sdks/permissions/README.md#remove) - Remove permissions
- [`permissionsUpdate`](docs/sdks/permissions/README.md#update) - Update permissions
- [`platformSettingsGet`](docs/sdks/platformsettings/README.md#get) - Get platform settings
- [`platformSettingsGetCustomSystemPrompt`](docs/sdks/platformsettings/README.md#getcustomsystemprompt) - Get custom system prompt
- [`platformSettingsGetFeatureFlags`](docs/sdks/platformsettings/README.md#getfeatureflags) - Get available feature flags
- [`platformSettingsUpdate`](docs/sdks/platformsettings/README.md#update) - Update platform settings
- [`platformSettingsUpdateSystemPrompt`](docs/sdks/platformsettings/README.md#updatesystemprompt) - Update custom system prompt
- [`publicUrlsGetConnector`](docs/sdks/publicurls/README.md#getconnector) - Get connector public URL
- [`publicUrlsGetFrontend`](docs/sdks/publicurls/README.md#getfrontend) - Get frontend public URL
- [`publicUrlsSetConnector`](docs/sdks/publicurls/README.md#setconnector) - Set connector public URL
- [`publicUrlsSetFrontendUrl`](docs/sdks/publicurls/README.md#setfrontendurl) - Set frontend public URL
- [`queryServiceChat`](docs/sdks/queryservice/README.md#chat) - [Query Service] Chat with knowledge base
- [`queryServiceChatStream`](docs/sdks/queryservice/README.md#chatstream) - [Query Service] Streaming chat with knowledge base
- [`queryServiceHealthCheck`](docs/sdks/queryservice/README.md#healthcheck) - [Query Service] AI model health check
- [`queryServiceListTools`](docs/sdks/queryservice/README.md#listtools) - [Query Service] List available agent tools
- [`queryServiceSearch`](docs/sdks/queryservice/README.md#search) - [Query Service] Semantic search
- [`queryServicesGetHealth`](docs/sdks/queryservices/README.md#gethealth) - [Query Service] Health check
- [`queueManagementGetStats`](docs/sdks/queuemanagement/README.md#getstats) - Get queue statistics
- [`recordsDelete`](docs/sdks/records/README.md#delete) - Delete record
- [`recordsGet`](docs/sdks/records/README.md#get) - Get all records across knowledge bases
- [`recordsGetById`](docs/sdks/records/README.md#getbyid) - Get record by ID
- [`recordsList`](docs/sdks/records/README.md#list) - Get records for a knowledge base
- [`recordsMove`](docs/sdks/records/README.md#move) - Move a record to another folder
- [`recordsStreamContent`](docs/sdks/records/README.md#streamcontent) - Stream record content
- [`recordsUpdate`](docs/sdks/records/README.md#update) - Update record
- [`samlCallback`](docs/sdks/saml/README.md#callback) - SAML authentication callback
- [`samlSignIn`](docs/sdks/saml/README.md#signin) - Initiate SAML sign-in flow
- [`samlUpdateAppConfig`](docs/sdks/saml/README.md#updateappconfig) - Reload SAML application configuration (Internal)
- [`semanticSearchArchive`](docs/sdks/semanticsearch/README.md#archive) - Archive search
- [`semanticSearchDelete`](docs/sdks/semanticsearch/README.md#delete) - Delete search
- [`semanticSearchDeleteAllHistory`](docs/sdks/semanticsearch/README.md#deleteallhistory) - Clear all search history
- [`semanticSearchGetById`](docs/sdks/semanticsearch/README.md#getbyid) - Get search by ID
- [`semanticSearchGetHistory`](docs/sdks/semanticsearch/README.md#gethistory) - Get search history
- [`semanticSearchPatchShare`](docs/sdks/semanticsearch/README.md#patchshare) - Share search results
- [`semanticSearchPostSearch`](docs/sdks/semanticsearch/README.md#postsearch) - Perform semantic search
- [`semanticSearchUnarchive`](docs/sdks/semanticsearch/README.md#unarchive) - Unarchive search
- [`semanticSearchUnshare`](docs/sdks/semanticsearch/README.md#unshare) - Revoke search access
- [`smtpConfigurationCreateOrUpdate`](docs/sdks/smtpconfiguration/README.md#createorupdate) - Create or update SMTP configuration
- [`smtpConfigurationGet`](docs/sdks/smtpconfiguration/README.md#get) - Get SMTP configuration
- [`storageConfigurationConfigureLocal`](docs/sdks/storageconfiguration/README.md#configurelocal) - Configure Local Storage
- [`storageConfigurationCreateAzureBlob`](docs/sdks/storageconfiguration/README.md#createazureblob) - Configure Azure Blob Storage
- [`storageConfigurationCreateS3StorageConfig`](docs/sdks/storageconfiguration/README.md#creates3storageconfig) - Configure AWS S3 Storage
- [`storageConfigurationGet`](docs/sdks/storageconfiguration/README.md#get) - Get current storage configuration
- [`teamsAddUsers`](docs/sdks/teams/README.md#addusers) - Add users to team
- [`teamsCreate`](docs/sdks/teams/README.md#create) - Create a team
- [`teamsDelete`](docs/sdks/teams/README.md#delete) - Delete team
- [`teamsGet`](docs/sdks/teams/README.md#get) - Get team by ID
- [`teamsGetCreatedByUser`](docs/sdks/teams/README.md#getcreatedbyuser) - Get teams created by current user
- [`teamsGetUser`](docs/sdks/teams/README.md#getuser) - Get current user's teams
- [`teamsGetUsers`](docs/sdks/teams/README.md#getusers) - Get team members
- [`teamsList`](docs/sdks/teams/README.md#list) - List teams
- [`teamsRemoveUsers`](docs/sdks/teams/README.md#removeusers) - Remove users from team
- [`teamsUpdate`](docs/sdks/teams/README.md#update) - Update team
- [`teamsUpdatePermissions`](docs/sdks/teams/README.md#updatepermissions) - Update user role in team
- [`uploadFiles`](docs/sdks/upload/README.md#files) - Upload files to knowledge base
- [`uploadGetLimits`](docs/sdks/upload/README.md#getlimits) - Get upload limits
- [`uploadToFolder`](docs/sdks/upload/README.md#tofolder) - Upload files to folder
- [`userAccountAuthenticate`](docs/sdks/useraccount/README.md#authenticate) - Authenticate user with credentials
- [`userAccountCheckPasswordStatus`](docs/sdks/useraccount/README.md#checkpasswordstatus) - Check if user has password set (Internal)
- [`userAccountForgotPassword`](docs/sdks/useraccount/README.md#forgotpassword) - Request password reset email
- [`userAccountGenerateLoginOtp`](docs/sdks/useraccount/README.md#generateloginotp) - Generate and send OTP for login
- [`userAccountInitializeAuth`](docs/sdks/useraccount/README.md#initializeauth) - Initialize authentication session
- [`userAccountLogout`](docs/sdks/useraccount/README.md#logout) - Logout current session
- [`userAccountRefresh`](docs/sdks/useraccount/README.md#refresh) - Refresh access token
- [`userAccountResetPassword`](docs/sdks/useraccount/README.md#resetpassword) - Reset password (authenticated user)
- [`userAccountResetPasswordWithToken`](docs/sdks/useraccount/README.md#resetpasswordwithtoken) - Reset password with email token
- [`userGroupsAddUsers`](docs/sdks/usergroups/README.md#addusers) - Add users to group
- [`userGroupsCreate`](docs/sdks/usergroups/README.md#create) - Create user group
- [`userGroupsDelete`](docs/sdks/usergroups/README.md#delete) - Delete user group
- [`userGroupsGetById`](docs/sdks/usergroups/README.md#getbyid) - Get user group by ID
- [`userGroupsGetStats`](docs/sdks/usergroups/README.md#getstats) - Get user group statistics
- [`userGroupsGetUserGroups`](docs/sdks/usergroups/README.md#getusergroups) - Get groups for a user
- [`userGroupsGetUsers`](docs/sdks/usergroups/README.md#getusers) - Get users in a group
- [`userGroupsList`](docs/sdks/usergroups/README.md#list) - Get all user groups
- [`userGroupsRemoveUsers`](docs/sdks/usergroups/README.md#removeusers) - Remove users from group
- [`userGroupsUpdate`](docs/sdks/usergroups/README.md#update) - Update user group
- [`usersBulkInvite`](docs/sdks/users/README.md#bulkinvite) - Bulk invite users
- [`usersCheckExistsByEmail`](docs/sdks/users/README.md#checkexistsbyemail) - Check if user exists by email
- [`usersCheckIsAdmin`](docs/sdks/users/README.md#checkisadmin) - Check if user is admin
- [`usersCreate`](docs/sdks/users/README.md#create) - Create a new user
- [`usersDelete`](docs/sdks/users/README.md#delete) - Delete user
- [`usersFetchWithGroups`](docs/sdks/users/README.md#fetchwithgroups) - Get all users with their groups
- [`usersGet`](docs/sdks/users/README.md#get) - Get all users
- [`usersGetById`](docs/sdks/users/README.md#getbyid) - Get user by ID
- [`usersGetByIds`](docs/sdks/users/README.md#getbyids) - Get users by IDs (bulk)
- [`usersGetDisplayPicture`](docs/sdks/users/README.md#getdisplaypicture) - Get display picture
- [`usersGetEmail`](docs/sdks/users/README.md#getemail) - Get user email by ID
- [`usersGetInternal`](docs/sdks/users/README.md#getinternal) - Get user (internal service-to-service)
- [`usersListGraph`](docs/sdks/users/README.md#listgraph) - List users (paginated with graph data)
- [`usersListTeams`](docs/sdks/users/README.md#listteams) - Get current user's teams
- [`usersRemoveDisplayPicture`](docs/sdks/users/README.md#removedisplaypicture) - Remove display picture
- [`usersResendInvite`](docs/sdks/users/README.md#resendinvite) - Resend user invite
- [`usersUpdate`](docs/sdks/users/README.md#update) - Update user
- [`usersUpdateDesignation`](docs/sdks/users/README.md#updatedesignation) - Update user designation
- [`usersUpdateFirstName`](docs/sdks/users/README.md#updatefirstname) - Update user first name
- [`usersUpdateFullName`](docs/sdks/users/README.md#updatefullname) - Update user full name
- [`usersUpdateLastName`](docs/sdks/users/README.md#updatelastname) - Update user last name
- [`usersUploadDisplayPicture`](docs/sdks/users/README.md#uploaddisplaypicture) - Upload display picture
- [`versionControlCheckModified`](docs/sdks/versioncontrol/README.md#checkmodified) - Check if document is modified
- [`versionControlRollBack`](docs/sdks/versioncontrol/README.md#rollback) - Rollback to previous version
- [`versionControlUploadNext`](docs/sdks/versioncontrol/README.md#uploadnext) - Upload next version
- [`webhooksHandle`](docs/sdks/webhooks/README.md#handle) - [Connector Service] Google Workspace Admin webhook
- [`webhooksPostGmail`](docs/sdks/webhooks/README.md#postgmail) - [Connector Service] Gmail webhook
- [`webhooksVerifyGmail`](docs/sdks/webhooks/README.md#verifygmail) - [Connector Service] Gmail webhook verification

</details>
<!-- End Standalone functions [standalone-funcs] -->

<!-- Start Server-sent event streaming [eventstream] -->
## Server-sent event streaming

[Server-sent events][mdn-sse] are used to stream content from certain
operations. These operations will expose the stream as an async iterable that
can be consumed using a [`for await...of`][mdn-for-await-of] loop. The loop will
terminate when the server no longer has any events to send and closes the
underlying connection.

```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.conversations.stream({
    query: "What are the key findings from our Q4 financial report?",
    recordIds: [
      "507f1f77bcf86cd799439011",
      "507f1f77bcf86cd799439012",
    ],
    modelKey: "gpt-4-turbo",
    modelName: "GPT-4 Turbo",
    chatMode: "balanced",
  });

  for await (const event of result) {
    console.log(event);
  }
}

run();

```

[mdn-sse]: https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events/Using_server-sent_events
[mdn-for-await-of]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for-await...of
<!-- End Server-sent event streaming [eventstream] -->

<!-- Start File uploads [file-upload] -->
## File uploads

Certain SDK methods accept files as part of a multi-part request. It is possible and typically recommended to upload files as a stream rather than reading the entire contents into memory. This avoids excessive memory consumption and potentially crashing with out-of-memory errors when working with very large files. The following example demonstrates how to attach a file stream to a request.

> [!TIP]
>
> Depending on your JavaScript runtime, there are convenient utilities that return a handle to a file without reading the entire contents into memory:
>
> - **Node.js v20+:** Since v20, Node.js comes with a native `openAsBlob` function in [`node:fs`](https://nodejs.org/docs/latest-v20.x/api/fs.html#fsopenasblobpath-options).
> - **Bun:** The native [`Bun.file`](https://bun.sh/docs/api/file-io#reading-files-bun-file) function produces a file handle that can be used for streaming file uploads.
> - **Browsers:** All supported browsers return an instance to a [`File`](https://developer.mozilla.org/en-US/docs/Web/API/File) when reading the value from an `<input type="file">` element.
> - **Node.js v18:** A file stream can be created using the `fileFrom` helper from [`fetch-blob/from.js`](https://www.npmjs.com/package/fetch-blob).

```typescript
import { openAsBlob } from "node:fs";
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.users.uploadDisplayPicture({
    file: await openAsBlob("example.file"),
  });

  console.log(result);
}

run();

```
<!-- End File uploads [file-upload] -->

<!-- Start Retries [retries] -->
## Retries

Some of the endpoints in this SDK support retries.  If you use the SDK without any configuration, it will fall back to the default retry strategy provided by the API.  However, the default retry strategy can be overridden on a per-operation basis, or across the entire SDK.

To change the default retry strategy for a single API call, simply provide a retryConfig object to the call:
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
});

async function run() {
  const result = await pipeshub.userAccount.initializeAuth({
    email: "user@example.com",
  }, {
    retries: {
      strategy: "backoff",
      backoff: {
        initialInterval: 1,
        maxInterval: 50,
        exponent: 1.1,
        maxElapsedTime: 100,
      },
      retryConnectionErrors: false,
    },
  });

  console.log(result);
}

run();

```

If you'd like to override the default retry strategy for all operations that support retries, you can provide a retryConfig at SDK initialization:
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  retryConfig: {
    strategy: "backoff",
    backoff: {
      initialInterval: 1,
      maxInterval: 50,
      exponent: 1.1,
      maxElapsedTime: 100,
    },
    retryConnectionErrors: false,
  },
});

async function run() {
  const result = await pipeshub.userAccount.initializeAuth({
    email: "user@example.com",
  });

  console.log(result);
}

run();

```
<!-- End Retries [retries] -->

<!-- Start Error Handling [errors] -->
## Error Handling

[`PipeshubError`](./src/models/errors/pipeshub-error.ts) is the base class for all HTTP error responses. It has the following properties:

| Property            | Type       | Description                                                                             |
| ------------------- | ---------- | --------------------------------------------------------------------------------------- |
| `error.message`     | `string`   | Error message                                                                           |
| `error.statusCode`  | `number`   | HTTP response status code eg `404`                                                      |
| `error.headers`     | `Headers`  | HTTP response headers                                                                   |
| `error.body`        | `string`   | HTTP body. Can be empty string if no body is returned.                                  |
| `error.rawResponse` | `Response` | Raw HTTP response                                                                       |
| `error.data$`       |            | Optional. Some errors may contain structured data. [See Error Classes](#error-classes). |

### Example
```typescript
import { Pipeshub } from "pipeshub";
import * as errors from "pipeshub/models/errors";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
});

async function run() {
  try {
    const result = await pipeshub.userAccount.initializeAuth({
      email: "user@example.com",
    });

    console.log(result);
  } catch (error) {
    // The base class for HTTP error responses
    if (error instanceof errors.PipeshubError) {
      console.log(error.message);
      console.log(error.statusCode);
      console.log(error.body);
      console.log(error.headers);

      // Depending on the method different errors may be thrown
      if (error instanceof errors.AuthError) {
        console.log(error.data$.error); // string
        console.log(error.data$.message); // string
        console.log(error.data$.code); // string
        console.log(error.data$.statusCode); // number
      }
    }
  }
}

run();

```

### Error Classes
**Primary error:**
* [`PipeshubError`](./src/models/errors/pipeshub-error.ts): The base class for HTTP error responses.

<details><summary>Less common errors (13)</summary>

<br />

**Network errors:**
* [`ConnectionError`](./src/models/errors/http-client-errors.ts): HTTP client was unable to make a request to a server.
* [`RequestTimeoutError`](./src/models/errors/http-client-errors.ts): HTTP request timed out due to an AbortSignal signal.
* [`RequestAbortedError`](./src/models/errors/http-client-errors.ts): HTTP request was aborted by the client.
* [`InvalidRequestError`](./src/models/errors/http-client-errors.ts): Any input used to create a request is invalid.
* [`UnexpectedClientError`](./src/models/errors/http-client-errors.ts): Unrecognised or unexpected error.


**Inherit from [`PipeshubError`](./src/models/errors/pipeshub-error.ts)**:
* [`AuthError`](./src/models/errors/auth-error.ts): Authentication error response with details for debugging and user feedback.<br><br> <b>Common Error Codes:</b><br> <ul> <li><code>INVALID_CREDENTIALS</code> - Wrong password or OTP</li> <li><code>ACCOUNT_BLOCKED</code> - Account locked after 5 failed attempts</li> <li><code>SESSION_EXPIRED</code> - Session token has expired</li> <li><code>OTP_EXPIRED</code> - OTP code has expired (10 min validity)</li> <li><code>USER_NOT_FOUND</code> - Email not registered</li> <li><code>INVALID_TOKEN</code> - JWT token is invalid or malformed</li> <li><code>METHOD_NOT_ALLOWED</code> - Auth method not enabled for org</li> </ul>. Applicable to 10 of 286 methods.*
* [`OAuthErrorResponse`](./src/models/errors/o-auth-error-response.ts): OAuth 2.0 Error Response (RFC 6749 Section 5.2). Standard error format for OAuth endpoints. Applicable to 5 of 286 methods.*
* [`BadRequestError`](./src/models/errors/bad-request-error.ts): Bad request. Possible reasons:<br> <ul> <li>SMTP not configured properly (missing host, port, or fromEmail)</li> <li>Invalid or unknown email template type</li> <li>Missing required templateData fields for the selected template</li> <li>Invalid email format in sendEmailTo or sendCcTo</li> </ul>. Status code `400`. Applicable to 1 of 286 methods.*
* [`NotFoundError`](./src/models/errors/not-found-error.ts): SMTP configuration not found in application config. Status code `404`. Applicable to 1 of 286 methods.*
* [`SendEmailInternalServerError`](./src/models/errors/send-email-internal-server-error.ts): Internal server error. Email sending failed due to:<br> <ul> <li>SMTP server connection failure</li> <li>Authentication failure with SMTP server</li> <li>Template compilation error</li> <li>Network issues</li> </ul>. Status code `500`. Applicable to 1 of 286 methods.*
* [`FailError`](./src/models/errors/fail-error.ts): Service is unhealthy or dependency check failed. Status code `500`. Applicable to 1 of 286 methods.*
* [`QueryServiceHealthCheckInternalServerError`](./src/models/errors/query-service-health-check-internal-server-error.ts): Model health check failed. Status code `500`. Applicable to 1 of 286 methods.*
* [`ResponseValidationError`](./src/models/errors/response-validation-error.ts): Type mismatch between the data returned from the server and the structure expected by the SDK. See `error.rawValue` for the raw value and `error.pretty()` for a nicely formatted multi-line string.

</details>

\* Check [the method documentation](#available-resources-and-operations) to see if the error is applicable.
<!-- End Error Handling [errors] -->

<!-- Start Custom HTTP Client [http-client] -->
## Custom HTTP Client

The TypeScript SDK makes API calls using an `HTTPClient` that wraps the native
[Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API). This
client is a thin wrapper around `fetch` and provides the ability to attach hooks
around the request lifecycle that can be used to modify the request or handle
errors and response.

The `HTTPClient` constructor takes an optional `fetcher` argument that can be
used to integrate a third-party HTTP client or when writing tests to mock out
the HTTP client and feed in fixtures.

The following example shows how to:
- route requests through a proxy server using [undici](https://www.npmjs.com/package/undici)'s ProxyAgent
- use the `"beforeRequest"` hook to add a custom header and a timeout to requests
- use the `"requestError"` hook to log errors

```typescript
import { Pipeshub } from "pipeshub";
import { ProxyAgent } from "undici";
import { HTTPClient } from "pipeshub/lib/http";

const dispatcher = new ProxyAgent("http://proxy.example.com:8080");

const httpClient = new HTTPClient({
  // 'fetcher' takes a function that has the same signature as native 'fetch'.
  fetcher: (input, init) =>
    // 'dispatcher' is specific to undici and not part of the standard Fetch API.
    fetch(input, { ...init, dispatcher } as RequestInit),
});

httpClient.addHook("beforeRequest", (request) => {
  const nextRequest = new Request(request, {
    signal: request.signal || AbortSignal.timeout(5000)
  });

  nextRequest.headers.set("x-custom-header", "custom value");

  return nextRequest;
});

httpClient.addHook("requestError", (error, request) => {
  console.group("Request Error");
  console.log("Reason:", `${error}`);
  console.log("Endpoint:", `${request.method} ${request.url}`);
  console.groupEnd();
});

const sdk = new Pipeshub({ httpClient: httpClient });
```
<!-- End Custom HTTP Client [http-client] -->

<!-- Start Debugging [debug] -->
## Debugging

You can setup your SDK to emit debug logs for SDK requests and responses.

You can pass a logger that matches `console`'s interface as an SDK option.

> [!WARNING]
> Beware that debug logging will reveal secrets, like API tokens in headers, in log messages printed to a console or files. It's recommended to use this feature only during local development and not in production.

```typescript
import { Pipeshub } from "pipeshub";

const sdk = new Pipeshub({ debugLogger: console });
```

You can also enable a default debug logger by setting an environment variable `PIPESHUB_DEBUG` to true.
<!-- End Debugging [debug] -->

<!-- Placeholder for Future Speakeasy SDK Sections -->
