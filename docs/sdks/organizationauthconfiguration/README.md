# OrganizationAuthConfiguration

## Overview

### Available Operations

* [updateMethod](#updatemethod) - Update organization authentication methods

## updateMethod

Update the authentication methods configuration for an organization.
This allows admins to configure single or multi-factor authentication.
<br><br>
<b>Validation Rules:</b><br>
- Minimum 1 step, maximum 3 steps<br>
- Each step must have a unique order (1, 2, or 3)<br>
- No duplicate methods within the same step<br>
- No method can appear in multiple steps<br>
- Each step must have at least one allowed method
<br><br>
<b>Available Methods:</b><br>
- <code>password</code>: Email/password authentication<br>
- <code>otp</code>: One-time password via email<br>
- <code>google</code>: Google OAuth 2.0<br>
- <code>microsoft</code>: Microsoft OAuth 2.0<br>
- <code>azureAd</code>: Azure Active Directory<br>
- <code>samlSso</code>: SAML 2.0 Single Sign-On<br>
- <code>oauth</code>: Generic OAuth 2.0 provider
<br><br>
<b>Example - Single Factor (Password or Google):</b><br>
<pre>
{
  "authMethods": [
    { "order": 1, "allowedMethods": [{ "type": "password" }, { "type": "google" }] }
  ]
}
</pre>
<br>
<b>Example - Two Factor (Password + OTP):</b><br>
<pre>
{
  "authMethods": [
    { "order": 1, "allowedMethods": [{ "type": "password" }] },
    { "order": 2, "allowedMethods": [{ "type": "otp" }] }
  ]
}
</pre>
<br>
<b>Admin Access Required:</b> Only organization admins can update auth configuration.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="updateAuthMethod" method="post" path="/orgAuthConfig/updateAuthMethod" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.organizationAuthConfiguration.updateMethod({
    authMethods: [
      {
        order: 195644,
        allowedMethods: [
          {
            type: "samlSso",
          },
        ],
      },
    ],
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { organizationAuthConfigurationUpdateMethod } from "pipeshub/funcs/organization-auth-configuration-update-method.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await organizationAuthConfigurationUpdateMethod(pipeshub, {
    authMethods: [
      {
        order: 195644,
        allowedMethods: [
          {
            type: "samlSso",
          },
        ],
      },
    ],
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("organizationAuthConfigurationUpdateMethod failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [models.AuthConfig](../../models/auth-config.md)                                                                                                                               | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.UpdateAuthMethodResponse](../../models/operations/update-auth-method-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.AuthError            | 400                         | application/json            |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |