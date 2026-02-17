# Saml

## Overview

### Available Operations

* [signIn](#signin) - Initiate SAML sign-in flow
* [callback](#callback) - SAML authentication callback
* [updateAppConfig](#updateappconfig) - Reload SAML application configuration (Internal)

## signIn

Initiate SAML Single Sign-On authentication by redirecting to the Identity Provider (IDP).
<br><br>
<b>Usage:</b><br>
1. Call <code>/userAccount/initAuth</code> to get a session token<br>
2. If <code>samlSso</code> is in the allowed methods, redirect the user to this endpoint<br>
3. User authenticates with their IDP<br>
4. IDP redirects back to <code>/saml/signIn/callback</code> with SAML response<br>
5. Callback completes authentication and returns tokens
<br><br>
<b>Note:</b> This is a browser redirect endpoint, not a typical API call.
The user's browser should be redirected to this URL.
<br><br>
<b>Prerequisites:</b><br>
- Organization must have SAML SSO configured via <code>/saml/updateAppConfig</code><br>
- User must belong to an organization with SAML enabled


### Example Usage

<!-- UsageSnippet language="typescript" operationID="signInViaSAML" method="get" path="/saml/signIn" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
});

async function run() {
  const result = await pipeshub.saml.signIn({
    email: "Daphney.Koss@hotmail.com",
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { samlSignIn } from "pipeshub/funcs/saml-sign-in.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
});

async function run() {
  const res = await samlSignIn(pipeshub, {
    email: "Daphney.Koss@hotmail.com",
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("samlSignIn failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.SignInViaSAMLRequest](../../models/operations/sign-in-via-saml-request.md)                                                                                         | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.SignInViaSAMLResponse](../../models/operations/sign-in-via-saml-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## callback

Handle the callback from SAML Identity Provider after user authentication.
This endpoint processes the SAML response and completes the authentication flow.
<br><br>
<b>Note:</b> This endpoint is called by the IDP, not directly by the client.
The IDP posts the SAML response to this URL after user authentication.
<br><br>
<b>Flow:</b><br>
1. IDP posts SAMLResponse and RelayState<br>
2. Server validates SAML assertion signature<br>
3. Server extracts user identity from assertion<br>
4. Server completes the authentication step<br>
5. Redirects to frontend with success/error status
<br><br>
<b>RelayState:</b> Contains the session token to resume the authentication flow.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="samlCallback" method="post" path="/saml/signIn/callback" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
});

async function run() {
  const result = await pipeshub.saml.callback();

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { samlCallback } from "pipeshub/funcs/saml-callback.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
});

async function run() {
  const res = await samlCallback(pipeshub);
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("samlCallback failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.SamlCallbackRequest](../../models/operations/saml-callback-request.md)                                                                                             | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.SamlCallbackResponse](../../models/operations/saml-callback-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.AuthError            | 400, 401                    | application/json            |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## updateAppConfig

Internal endpoint to reload SAML configuration from the configuration manager.
This is called by other services when SAML settings are updated.<br><br>
<b>Purpose:</b><br>
When SAML configuration is updated in the Configuration Manager, this endpoint
is called to reload the settings into the authentication service without restart.<br><br>
<b>Effects:</b><br>
<ul>
<li>Reloads AppConfig from configuration files</li>
<li>Rebinds authentication controllers with new config</li>
<li>Updates SAML passport strategy settings</li>
</ul>
<b>Note:</b> This is an internal service-to-service endpoint.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="updateSamlAppConfig" method="post" path="/saml/updateAppConfig" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
});

async function run() {
  const result = await pipeshub.saml.updateAppConfig({
    scopedToken: process.env["PIPESHUB_SCOPED_TOKEN"] ?? "",
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { samlUpdateAppConfig } from "pipeshub/funcs/saml-update-app-config.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
});

async function run() {
  const res = await samlUpdateAppConfig(pipeshub, {
    scopedToken: process.env["PIPESHUB_SCOPED_TOKEN"] ?? "",
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("samlUpdateAppConfig failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `security`                                                                                                                                                                     | [operations.UpdateSamlAppConfigSecurity](../../models/operations/update-saml-app-config-security.md)                                                                           | :heavy_check_mark:                                                                                                                                                             | The security requirements to use for the request.                                                                                                                              |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.UpdateSamlAppConfigResponse](../../models/operations/update-saml-app-config-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |