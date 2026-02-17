# ConnectorService

## Overview

### Available Operations

* [checkHealth](#checkhealth) - [Connector Service] Health check
* [postDrive](#postdrive) - [Connector Service] Google Drive webhook
* [internalStreamRecord](#internalstreamrecord) - [Connector Service] Internal stream record
* [convertRecordBuffer](#convertrecordbuffer) - [Connector Service] Convert record buffer
* [getStats](#getstats) - [Connector Service] Get connector statistics
* [getSignedUrl](#getsignedurl) - [Connector Service] Get signed URL for record

## checkHealth

⚠️ <b>INTERNAL SERVICE ENDPOINT</b><br><br>

Health check endpoint for the Connector Service (Python FastAPI).<br><br>

<b>Service:</b> Connector Service<br>
<b>Port:</b> 8088<br>
<b>Base URL:</b> <code>http://localhost:8088</code><br><br>

<b>Authentication:</b> None required for health check<br><br>

<b>Note:</b> This is the core internal service that manages all
data source connectors and OAuth flows.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="connectorServiceHealth" method="get" path="/connector/health" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
});

async function run() {
  const result = await pipeshub.connectorService.checkHealth();

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { connectorServiceCheckHealth } from "pipeshub/funcs/connector-service-check-health.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
});

async function run() {
  const res = await connectorServiceCheckHealth(pipeshub);
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("connectorServiceCheckHealth failed:", res.error);
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

**Promise\<[operations.ConnectorServiceHealthResponse](../../models/operations/connector-service-health-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## postDrive

⚠️ <b>INTERNAL SERVICE ENDPOINT</b><br><br>

Webhook endpoint for Google Drive push notifications.<br><br>

<b>Service:</b> Connector Service<br>
<b>Port:</b> 8088<br>
<b>Base URL:</b> <code>http://localhost:8088</code><br><br>

<b>Authentication:</b> None required - uses Google's push notification verification<br><br>

<b>Note:</b> This endpoint receives real-time change notifications from
Google Drive when files are created, modified, or deleted.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="driveWebhook" method="post" path="/connector/drive/webhook" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
});

async function run() {
  await pipeshub.connectorService.postDrive();


}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { connectorServicePostDrive } from "pipeshub/funcs/connector-service-post-drive.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
});

async function run() {
  const res = await connectorServicePostDrive(pipeshub);
  if (res.ok) {
    const { value: result } = res;
    
  } else {
    console.log("connectorServicePostDrive failed:", res.error);
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

## internalStreamRecord

⚠️ <b>INTERNAL SERVICE ENDPOINT</b><br><br>

Internal endpoint for streaming record content (service-to-service).<br><br>

<b>Service:</b> Connector Service<br>
<b>Port:</b> 8088<br>
<b>Base URL:</b> <code>http://localhost:8088</code><br><br>

<b>Authentication:</b> Requires scoped service token<br><br>

<b>Use Case:</b> Used by Indexing Service to fetch file content for processing.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="connectorInternalStreamRecord" method="get" path="/connector/api/v1/internal/stream/record/{record_id}" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
});

async function run() {
  const result = await pipeshub.connectorService.internalStreamRecord({
    scopedToken: process.env["PIPESHUB_SCOPED_TOKEN"] ?? "",
  }, {
    recordId: "<id>",
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { connectorServiceInternalStreamRecord } from "pipeshub/funcs/connector-service-internal-stream-record.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
});

async function run() {
  const res = await connectorServiceInternalStreamRecord(pipeshub, {
    scopedToken: process.env["PIPESHUB_SCOPED_TOKEN"] ?? "",
  }, {
    recordId: "<id>",
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("connectorServiceInternalStreamRecord failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.ConnectorInternalStreamRecordRequest](../../models/operations/connector-internal-stream-record-request.md)                                                         | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `security`                                                                                                                                                                     | [operations.ConnectorInternalStreamRecordSecurity](../../models/operations/connector-internal-stream-record-security.md)                                                       | :heavy_check_mark:                                                                                                                                                             | The security requirements to use for the request.                                                                                                                              |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |
| `options.serverURL`                                                                                                                                                            | *string*                                                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                             | An optional server URL to use.                                                                                                                                                 |

### Response

**Promise\<[ReadableStream<Uint8Array>](../../models/.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## convertRecordBuffer

⚠️ <b>INTERNAL SERVICE ENDPOINT</b><br><br>

Convert a record buffer to a different format.<br><br>

<b>Service:</b> Connector Service<br>
<b>Port:</b> 8088<br>
<b>Base URL:</b> <code>http://localhost:8088</code><br><br>

<b>Authentication:</b> Requires scoped service token<br><br>

<b>Supported Conversions:</b> PDF to text, DOCX to text, etc.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="connectorConvertRecordBuffer" method="post" path="/connector/api/v1/record/buffer/convert" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
});

async function run() {
  const result = await pipeshub.connectorService.convertRecordBuffer({
    scopedToken: process.env["PIPESHUB_SCOPED_TOKEN"] ?? "",
  }, {
    buffer: "<value>",
    convertTo: "<value>",
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { connectorServiceConvertRecordBuffer } from "pipeshub/funcs/connector-service-convert-record-buffer.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
});

async function run() {
  const res = await connectorServiceConvertRecordBuffer(pipeshub, {
    scopedToken: process.env["PIPESHUB_SCOPED_TOKEN"] ?? "",
  }, {
    buffer: "<value>",
    convertTo: "<value>",
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("connectorServiceConvertRecordBuffer failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.ConnectorConvertRecordBufferRequest](../../models/operations/connector-convert-record-buffer-request.md)                                                           | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `security`                                                                                                                                                                     | [operations.ConnectorConvertRecordBufferSecurity](../../models/operations/connector-convert-record-buffer-security.md)                                                         | :heavy_check_mark:                                                                                                                                                             | The security requirements to use for the request.                                                                                                                              |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |
| `options.serverURL`                                                                                                                                                            | *string*                                                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                             | An optional server URL to use.                                                                                                                                                 |

### Response

**Promise\<[ReadableStream<Uint8Array>](../../models/.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## getStats

⚠️ <b>INTERNAL SERVICE ENDPOINT</b><br><br>

Get statistics for a specific connector.<br><br>

<b>Service:</b> Connector Service<br>
<b>Port:</b> 8088<br>
<b>Base URL:</b> <code>http://localhost:8088</code><br><br>

<b>Authentication:</b> Requires scoped service token


### Example Usage

<!-- UsageSnippet language="typescript" operationID="connectorGetStats" method="get" path="/connector/api/v1/stats" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
});

async function run() {
  const result = await pipeshub.connectorService.getStats({
    scopedToken: process.env["PIPESHUB_SCOPED_TOKEN"] ?? "",
  }, {
    orgId: "<id>",
    connector: "<value>",
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { connectorServiceGetStats } from "pipeshub/funcs/connector-service-get-stats.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
});

async function run() {
  const res = await connectorServiceGetStats(pipeshub, {
    scopedToken: process.env["PIPESHUB_SCOPED_TOKEN"] ?? "",
  }, {
    orgId: "<id>",
    connector: "<value>",
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("connectorServiceGetStats failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.ConnectorGetStatsRequest](../../models/operations/connector-get-stats-request.md)                                                                                  | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `security`                                                                                                                                                                     | [operations.ConnectorGetStatsSecurity](../../models/operations/connector-get-stats-security.md)                                                                                | :heavy_check_mark:                                                                                                                                                             | The security requirements to use for the request.                                                                                                                              |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |
| `options.serverURL`                                                                                                                                                            | *string*                                                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                             | An optional server URL to use.                                                                                                                                                 |

### Response

**Promise\<[operations.ConnectorGetStatsResponse](../../models/operations/connector-get-stats-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## getSignedUrl

⚠️ <b>INTERNAL SERVICE ENDPOINT</b><br><br>

Get a signed URL for direct file access from the connector source.<br><br>

<b>Service:</b> Connector Service<br>
<b>Port:</b> 8088<br>
<b>Base URL:</b> <code>http://localhost:8088</code><br><br>

<b>Authentication:</b> Requires scoped service token<br><br>

<b>Use Case:</b> Generate temporary signed URLs for file downloads from
Google Drive, OneDrive, SharePoint, etc.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="connectorGetSignedUrl" method="get" path="/connector/api/v1/{org_id}/{user_id}/{connector}/record/{record_id}/signedUrl" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
});

async function run() {
  const result = await pipeshub.connectorService.getSignedUrl({
    scopedToken: process.env["PIPESHUB_SCOPED_TOKEN"] ?? "",
  }, {
    orgId: "<id>",
    userId: "<id>",
    connector: "<value>",
    recordId: "<id>",
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { connectorServiceGetSignedUrl } from "pipeshub/funcs/connector-service-get-signed-url.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
});

async function run() {
  const res = await connectorServiceGetSignedUrl(pipeshub, {
    scopedToken: process.env["PIPESHUB_SCOPED_TOKEN"] ?? "",
  }, {
    orgId: "<id>",
    userId: "<id>",
    connector: "<value>",
    recordId: "<id>",
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("connectorServiceGetSignedUrl failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.ConnectorGetSignedUrlRequest](../../models/operations/connector-get-signed-url-request.md)                                                                         | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `security`                                                                                                                                                                     | [operations.ConnectorGetSignedUrlSecurity](../../models/operations/connector-get-signed-url-security.md)                                                                       | :heavy_check_mark:                                                                                                                                                             | The security requirements to use for the request.                                                                                                                              |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |
| `options.serverURL`                                                                                                                                                            | *string*                                                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                             | An optional server URL to use.                                                                                                                                                 |

### Response

**Promise\<[operations.ConnectorGetSignedUrlResponse](../../models/operations/connector-get-signed-url-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |