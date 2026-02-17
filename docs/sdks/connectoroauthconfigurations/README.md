# ConnectorOAuthConfigurations

## Overview

### Available Operations

* [setGoogleWorkspaceOauth](#setgoogleworkspaceoauth) - Configure Google Workspace OAuth
* [configureOneDrive](#configureonedrive) - Configure OneDrive connector
* [setSharePointConfig](#setsharepointconfig) - Configure SharePoint connector

## setGoogleWorkspaceOauth

Set up OAuth credentials for Google Workspace connector. Required for user authentication with Google Drive, Gmail, etc.

### Example Usage

<!-- UsageSnippet language="typescript" operationID="setGoogleWorkspaceOauthConfig" method="post" path="/configurationManager/connectors/googleWorkspaceOauthConfig" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  await pipeshub.connectorOAuthConfigurations.setGoogleWorkspaceOauth({
    clientId: "<id>",
    clientSecret: "<value>",
  });


}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { connectorOAuthConfigurationsSetGoogleWorkspaceOauth } from "pipeshub/funcs/connector-o-auth-configurations-set-google-workspace-oauth.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await connectorOAuthConfigurationsSetGoogleWorkspaceOauth(pipeshub, {
    clientId: "<id>",
    clientSecret: "<value>",
  });
  if (res.ok) {
    const { value: result } = res;
    
  } else {
    console.log("connectorOAuthConfigurationsSetGoogleWorkspaceOauth failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [models.GoogleWorkspaceOAuthConfig](../../models/google-workspace-o-auth-config.md)                                                                                            | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<void\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## configureOneDrive

Set up Microsoft credentials for OneDrive connector.

### Example Usage

<!-- UsageSnippet language="typescript" operationID="setOneDriveConfig" method="post" path="/configurationManager/connectors/onedrive/config" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  await pipeshub.connectorOAuthConfigurations.configureOneDrive({
    clientId: "<id>",
    clientSecret: "<value>",
    tenantId: "<id>",
  });


}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { connectorOAuthConfigurationsConfigureOneDrive } from "pipeshub/funcs/connector-o-auth-configurations-configure-one-drive.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await connectorOAuthConfigurationsConfigureOneDrive(pipeshub, {
    clientId: "<id>",
    clientSecret: "<value>",
    tenantId: "<id>",
  });
  if (res.ok) {
    const { value: result } = res;
    
  } else {
    console.log("connectorOAuthConfigurationsConfigureOneDrive failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [models.OneDriveConfig](../../models/one-drive-config.md)                                                                                                                      | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<void\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## setSharePointConfig

Set up Microsoft credentials for SharePoint connector.

### Example Usage

<!-- UsageSnippet language="typescript" operationID="setSharePointConfig" method="post" path="/configurationManager/connectors/sharepoint/config" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  await pipeshub.connectorOAuthConfigurations.setSharePointConfig({
    clientId: "<id>",
    clientSecret: "<value>",
    tenantId: "<id>",
    sharepointDomain: "<value>",
  });


}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { connectorOAuthConfigurationsSetSharePointConfig } from "pipeshub/funcs/connector-o-auth-configurations-set-share-point-config.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await connectorOAuthConfigurationsSetSharePointConfig(pipeshub, {
    clientId: "<id>",
    clientSecret: "<value>",
    tenantId: "<id>",
    sharepointDomain: "<value>",
  });
  if (res.ok) {
    const { value: result } = res;
    
  } else {
    console.log("connectorOAuthConfigurationsSetSharePointConfig failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [models.SharePointConfig](../../models/share-point-config.md)                                                                                                                  | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<void\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |