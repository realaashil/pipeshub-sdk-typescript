# Webhooks

## Overview

Webhook handlers for real-time updates

### Available Operations

* [verifyGmail](#verifygmail) - [Connector Service] Gmail webhook verification
* [postGmail](#postgmail) - [Connector Service] Gmail webhook
* [handle](#handle) - [Connector Service] Google Workspace Admin webhook

## verifyGmail

⚠️ <b>INTERNAL SERVICE ENDPOINT</b><br><br>

GET handler for Gmail Pub/Sub webhook verification.<br><br>

<b>Service:</b> Connector Service<br>
<b>Port:</b> 8088<br>
<b>Base URL:</b> <code>http://localhost:8088</code><br><br>

<b>Authentication:</b> None required - uses Google Pub/Sub verification<br><br>

<b>Note:</b> Google Pub/Sub may send GET requests for subscription verification.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="gmailWebhookVerify" method="get" path="/connector/gmail/webhook" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
});

async function run() {
  await pipeshub.webhooks.verifyGmail();


}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { webhooksVerifyGmail } from "pipeshub/funcs/webhooks-verify-gmail.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
});

async function run() {
  const res = await webhooksVerifyGmail(pipeshub);
  if (res.ok) {
    const { value: result } = res;
    
  } else {
    console.log("webhooksVerifyGmail failed:", res.error);
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
| `options.serverURL`                                                                                                                                                            | *string*                                                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                             | An optional server URL to use.                                                                                                                                                 |

### Response

**Promise\<void\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## postGmail

⚠️ <b>INTERNAL SERVICE ENDPOINT</b><br><br>

Webhook endpoint for Gmail Pub/Sub notifications.<br><br>

<b>Service:</b> Connector Service<br>
<b>Port:</b> 8088<br>
<b>Base URL:</b> <code>http://localhost:8088</code><br><br>

<b>Authentication:</b> None required - uses Google Pub/Sub verification<br><br>

<b>Note:</b> This endpoint receives notifications when new emails arrive
or email labels change.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="gmailWebhook" method="post" path="/connector/gmail/webhook" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
});

async function run() {
  await pipeshub.webhooks.postGmail();


}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { webhooksPostGmail } from "pipeshub/funcs/webhooks-post-gmail.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
});

async function run() {
  const res = await webhooksPostGmail(pipeshub);
  if (res.ok) {
    const { value: result } = res;
    
  } else {
    console.log("webhooksPostGmail failed:", res.error);
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
| `options.serverURL`                                                                                                                                                            | *string*                                                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                             | An optional server URL to use.                                                                                                                                                 |

### Response

**Promise\<void\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## handle

⚠️ <b>INTERNAL SERVICE ENDPOINT</b><br><br>

Webhook endpoint for Google Workspace Admin push notifications.<br><br>

<b>Service:</b> Connector Service<br>
<b>Port:</b> 8088<br>
<b>Base URL:</b> <code>http://localhost:8088</code><br><br>

<b>Authentication:</b> Verified via Google Workspace webhook signature<br><br>

<b>Note:</b> This endpoint receives notifications about user and group
changes from Google Workspace Admin directory (e.g., user created,
deleted, suspended, group membership changes).


### Example Usage

<!-- UsageSnippet language="typescript" operationID="adminWebhook" method="post" path="/connector/admin/webhook" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
});

async function run() {
  await pipeshub.webhooks.handle();


}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { webhooksHandle } from "pipeshub/funcs/webhooks-handle.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
});

async function run() {
  const res = await webhooksHandle(pipeshub);
  if (res.ok) {
    const { value: result } = res;
    
  } else {
    console.log("webhooksHandle failed:", res.error);
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
| `options.serverURL`                                                                                                                                                            | *string*                                                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                             | An optional server URL to use.                                                                                                                                                 |

### Response

**Promise\<void\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |