# ConnectorConfiguration

## Overview

### Available Operations

* [get](#get) - Get connector configuration
* [update](#update) - Update connector configuration
* [updateFiltersSync](#updatefilterssync) - Update filters and sync configuration

## get

Get the current configuration for a connector instance.<br><br>
<b>Security:</b><br>
Sensitive data (credentials, OAuth tokens) are redacted from the response.
Only admins can see partial credential information.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="getConnectorConfig" method="get" path="/connectors/{connectorId}/config" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.connectorConfiguration.get({
    connectorId: "<id>",
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { connectorConfigurationGet } from "pipeshub/funcs/connector-configuration-get.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await connectorConfigurationGet(pipeshub, {
    connectorId: "<id>",
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("connectorConfigurationGet failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.GetConnectorConfigRequest](../../models/operations/get-connector-config-request.md)                                                                                | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.GetConnectorConfigResponse](../../models/operations/get-connector-config-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## update

Update authentication, sync, and filter configuration.<br><br>
<b>Prerequisites:</b><br>
Connector must be <b>disabled</b> before updating configuration.
Disable it first using <code>POST /{id}/toggle</code>.<br><br>
<b>Partial Updates:</b><br>
Only provide the sections you want to update. Omitted sections
are not modified.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="updateConnectorConfig" method="put" path="/connectors/{connectorId}/config" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.connectorConfiguration.update({
    connectorId: "<id>",
    body: {
      auth: {
        values: {
          "apiKey": "sk-xxxxx",
          "baseUrl": "https://api.example.com",
        },
        oauthConfigId: "oauth_config_123",
      },
      sync: {
        scheduledConfig: {
          cronExpression: "0 */6 * * *",
          timezone: "America/New_York",
        },
        webhookConfig: {
          events: [
            "file.created",
            "file.modified",
            "file.deleted",
          ],
        },
      },
      filters: {
        sync: {
          values: {
            "folders": [
              "folder_id_1",
              "folder_id_2",
            ],
            "fileTypes": [
              "pdf",
              "docx",
              "xlsx",
            ],
            "includeShared": true,
          },
        },
      },
      baseUrl: "https://confluence.mycompany.com",
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
import { connectorConfigurationUpdate } from "pipeshub/funcs/connector-configuration-update.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await connectorConfigurationUpdate(pipeshub, {
    connectorId: "<id>",
    body: {
      auth: {
        values: {
          "apiKey": "sk-xxxxx",
          "baseUrl": "https://api.example.com",
        },
        oauthConfigId: "oauth_config_123",
      },
      sync: {
        scheduledConfig: {
          cronExpression: "0 */6 * * *",
          timezone: "America/New_York",
        },
        webhookConfig: {
          events: [
            "file.created",
            "file.modified",
            "file.deleted",
          ],
        },
      },
      filters: {
        sync: {
          values: {
            "folders": [
              "folder_id_1",
              "folder_id_2",
            ],
            "fileTypes": [
              "pdf",
              "docx",
              "xlsx",
            ],
            "includeShared": true,
          },
        },
      },
      baseUrl: "https://confluence.mycompany.com",
    },
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("connectorConfigurationUpdate failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.UpdateConnectorConfigRequest](../../models/operations/update-connector-config-request.md)                                                                          | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.UpdateConnectorConfigResponse](../../models/operations/update-connector-config-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## updateFiltersSync

Update filter selections and sync settings without touching auth.<br><br>
<b>Use Case:</b><br>
Use this to change what data is synced or adjust sync schedule
without re-authenticating.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="updateConnectorFiltersSyncConfig" method="put" path="/connectors/{connectorId}/config/filters-sync" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.connectorConfiguration.updateFiltersSync({
    connectorId: "<id>",
    body: {
      sync: {
        scheduledConfig: {
          cronExpression: "0 */6 * * *",
          timezone: "America/New_York",
        },
        webhookConfig: {
          events: [
            "file.created",
            "file.modified",
            "file.deleted",
          ],
        },
      },
      filters: {
        sync: {
          values: {
            "folders": [
              "folder_id_1",
              "folder_id_2",
            ],
            "fileTypes": [
              "pdf",
              "docx",
              "xlsx",
            ],
            "includeShared": true,
          },
        },
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
import { connectorConfigurationUpdateFiltersSync } from "pipeshub/funcs/connector-configuration-update-filters-sync.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await connectorConfigurationUpdateFiltersSync(pipeshub, {
    connectorId: "<id>",
    body: {
      sync: {
        scheduledConfig: {
          cronExpression: "0 */6 * * *",
          timezone: "America/New_York",
        },
        webhookConfig: {
          events: [
            "file.created",
            "file.modified",
            "file.deleted",
          ],
        },
      },
      filters: {
        sync: {
          values: {
            "folders": [
              "folder_id_1",
              "folder_id_2",
            ],
            "fileTypes": [
              "pdf",
              "docx",
              "xlsx",
            ],
            "includeShared": true,
          },
        },
      },
    },
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("connectorConfigurationUpdateFiltersSync failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.UpdateConnectorFiltersSyncConfigRequest](../../models/operations/update-connector-filters-sync-config-request.md)                                                  | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.UpdateConnectorFiltersSyncConfigResponse](../../models/operations/update-connector-filters-sync-config-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |