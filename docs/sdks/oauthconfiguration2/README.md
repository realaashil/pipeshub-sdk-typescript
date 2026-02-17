# OAuthConfiguration

## Overview

### Available Operations

* [create](#create) - Create OAuth configuration

## create

Create a new OAuth configuration for a connector type.<br><br>
<b>Admin Only:</b><br>
Only admins can create OAuth configurations. These provide the
OAuth credentials needed for users to authenticate connectors.<br><br>
<b>Use Case:</b><br>
Before users can create Google Drive connectors with OAuth,
an admin must create an OAuth configuration with the Google
OAuth client ID and secret.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="createOAuthConfig" method="post" path="/oauth/{connectorType}" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.oAuthConfiguration.create({
    connectorType: "<value>",
    body: {
      oauthInstanceName: "Production Google OAuth Credentials",
      config: {
        clientId: "123456789-abc.apps.googleusercontent.com",
        clientSecret: "GOCSPX-xxxxxxxxxxxxx",
        tenantId: "12345678-1234-1234-1234-123456789abc",
      },
      baseUrl: "https://gitlab.mycompany.com",
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
import { oAuthConfigurationCreate } from "pipeshub/funcs/o-auth-configuration-create.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await oAuthConfigurationCreate(pipeshub, {
    connectorType: "<value>",
    body: {
      oauthInstanceName: "Production Google OAuth Credentials",
      config: {
        clientId: "123456789-abc.apps.googleusercontent.com",
        clientSecret: "GOCSPX-xxxxxxxxxxxxx",
        tenantId: "12345678-1234-1234-1234-123456789abc",
      },
      baseUrl: "https://gitlab.mycompany.com",
    },
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("oAuthConfigurationCreate failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.CreateOAuthConfigRequest](../../models/operations/create-o-auth-config-request.md)                                                                                 | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.CreateOAuthConfigResponse](../../models/operations/create-o-auth-config-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |