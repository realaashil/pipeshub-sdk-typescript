# ConnectorConfigurations

## Overview

### Available Operations

* [updateAuth](#updateauth) - Update authentication configuration
* [getGoogleWorkspaceCredentials](#getgoogleworkspacecredentials) - Get Google Workspace credentials status

## updateAuth

Update only the authentication configuration.<br><br>
<b>Use Case:</b><br>
Use this when you need to update credentials without changing
sync or filter settings. Useful for credential rotation.<br><br>
<b>Prerequisites:</b><br>
Connector must be disabled. This endpoint clears OAuth state,
requiring re-authentication for OAuth connectors.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="updateConnectorAuthConfig" method="put" path="/connectors/{connectorId}/config/auth" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.connectorConfigurations.updateAuth({
    connectorId: "<id>",
    body: {
      auth: {
        values: {
          "apiKey": "sk-xxxxx",
          "baseUrl": "https://api.example.com",
        },
        oauthConfigId: "oauth_config_123",
      },
    },
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { connectorConfigurationsUpdateAuth } from "pipeshub/funcs/connector-configurations-update-auth.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await connectorConfigurationsUpdateAuth(pipeshub, {
    connectorId: "<id>",
    body: {
      auth: {
        values: {
          "apiKey": "sk-xxxxx",
          "baseUrl": "https://api.example.com",
        },
        oauthConfigId: "oauth_config_123",
      },
    },
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("connectorConfigurationsUpdateAuth failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.UpdateConnectorAuthConfigRequest](../../models/operations/update-connector-auth-config-request.md)                                                                 | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.UpdateConnectorAuthConfigResponse](../../models/operations/update-connector-auth-config-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## getGoogleWorkspaceCredentials

Check if Google Workspace credentials are configured.

### Example Usage

<!-- UsageSnippet language="typescript" operationID="getGoogleWorkspaceCredentials" method="get" path="/configurationManager/connectors/googleWorkspaceCredentials" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.connectorConfigurations.getGoogleWorkspaceCredentials();

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { connectorConfigurationsGetGoogleWorkspaceCredentials } from "pipeshub/funcs/connector-configurations-get-google-workspace-credentials.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await connectorConfigurationsGetGoogleWorkspaceCredentials(pipeshub);
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("connectorConfigurationsGetGoogleWorkspaceCredentials failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[models.GoogleWorkspaceCredentials](../../models/google-workspace-credentials.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |