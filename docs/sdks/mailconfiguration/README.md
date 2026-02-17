# MailConfiguration

## Overview

### Available Operations

* [updateSmtp](#updatesmtp) - Reload SMTP configuration

## updateSmtp

Dynamically reload the SMTP configuration from the application config file without restarting the service.<br><br>

<b>Overview:</b><br>
This internal endpoint allows the mail service to pick up SMTP configuration changes at runtime.
When SMTP settings are updated via <code>/configurationManager/smtpConfig</code>, this endpoint
should be called to apply the changes to the running mail service.<br><br>

<b>Authentication:</b><br>
Requires a scoped token with <code>fetch:config</code> scope. This endpoint is designed for
internal service communication only.<br><br>

<b>How It Works:</b><br>
<ol>
<li>Reads the latest configuration from the config file/etcd</li>
<li>Rebinds the AppConfig in the dependency injection container</li>
<li>Creates a new MailController instance with updated config</li>
<li>Returns the new SMTP configuration (excluding password)</li>
</ol>

<b>Use Cases:</b><br>
<ul>
<li>Apply SMTP configuration changes without service restart</li>
<li>Switch SMTP providers at runtime</li>
<li>Update SMTP credentials</li>
<li>Change sender email address</li>
</ul>

<b>Related Endpoints:</b><br>
<ul>
<li><code>POST /configurationManager/smtpConfig</code> - Create/update SMTP configuration</li>
<li><code>GET /configurationManager/smtpConfig</code> - Get current SMTP configuration</li>
</ul>


### Example Usage

<!-- UsageSnippet language="typescript" operationID="updateSmtpConfig" method="post" path="/mail/updateSmtpConfig" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
});

async function run() {
  const result = await pipeshub.mailConfiguration.updateSmtp({
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
import { mailConfigurationUpdateSmtp } from "pipeshub/funcs/mail-configuration-update-smtp.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
});

async function run() {
  const res = await mailConfigurationUpdateSmtp(pipeshub, {
    scopedToken: process.env["PIPESHUB_SCOPED_TOKEN"] ?? "",
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("mailConfigurationUpdateSmtp failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `security`                                                                                                                                                                     | [operations.UpdateSmtpConfigSecurity](../../models/operations/update-smtp-config-security.md)                                                                                  | :heavy_check_mark:                                                                                                                                                             | The security requirements to use for the request.                                                                                                                              |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.UpdateSmtpConfigResponse](../../models/operations/update-smtp-config-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |