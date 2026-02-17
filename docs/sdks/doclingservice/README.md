# DoclingService

## Overview

### Available Operations

* [healthCheck](#healthcheck) - [Docling Service] Health check
* [processPdf](#processpdf) - [Docling Service] Process PDF document
* [parsePdf](#parsepdf) - [Docling Service] Parse PDF (Phase 1)
* [createBlocks](#createblocks) - [Docling Service] Create blocks from parse result (Phase 2)

## healthCheck

⚠️ <b>INTERNAL SERVICE ENDPOINT</b><br><br>

Health check endpoint for the Docling Service (Python FastAPI).<br><br>

<b>Service:</b> Docling Service<br>
<b>Port:</b> 8081<br>
<b>Base URL:</b> <code>http://localhost:8081</code><br><br>

<b>Authentication:</b> None required for health check<br><br>

<b>Note:</b> This is an internal service used by the Indexing Service
for advanced document parsing. No user-facing endpoints.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="doclingServiceHealth" method="get" path="/docling/health" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
});

async function run() {
  const result = await pipeshub.doclingService.healthCheck();

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { doclingServiceHealthCheck } from "pipeshub/funcs/docling-service-health-check.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
});

async function run() {
  const res = await doclingServiceHealthCheck(pipeshub);
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("doclingServiceHealthCheck failed:", res.error);
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

**Promise\<[operations.DoclingServiceHealthResponse](../../models/operations/docling-service-health-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## processPdf

⚠️ <b>INTERNAL SERVICE ENDPOINT</b><br><br>

Full PDF processing endpoint - parses PDF and creates content blocks.<br><br>

<b>Service:</b> Docling Service<br>
<b>Port:</b> 8081<br>
<b>Base URL:</b> <code>http://localhost:8081</code><br><br>

<b>Authentication:</b> Internal only - called by Indexing Service<br><br>

<b>Processing Steps:</b>
<ol>
<li>Decode base64 PDF binary</li>
<li>Parse document structure using Docling library</li>
<li>Extract text, tables, and images</li>
<li>Create content blocks for indexing</li>
</ol>

<b>Timeout:</b> 40 minutes (for large documents)


### Example Usage

<!-- UsageSnippet language="typescript" operationID="doclingProcessPdf" method="post" path="/docling/process-pdf" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
});

async function run() {
  const result = await pipeshub.doclingService.processPdf({
    recordName: "<value>",
    pdfBinary: "<value>",
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { doclingServiceProcessPdf } from "pipeshub/funcs/docling-service-process-pdf.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
});

async function run() {
  const res = await doclingServiceProcessPdf(pipeshub, {
    recordName: "<value>",
    pdfBinary: "<value>",
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("doclingServiceProcessPdf failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.DoclingProcessPdfRequest](../../models/operations/docling-process-pdf-request.md)                                                                                  | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |
| `options.serverURL`                                                                                                                                                            | *string*                                                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                             | An optional server URL to use.                                                                                                                                                 |

### Response

**Promise\<[operations.DoclingProcessPdfResponse](../../models/operations/docling-process-pdf-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## parsePdf

⚠️ <b>INTERNAL SERVICE ENDPOINT</b><br><br>

Phase 1 of two-phase PDF processing - parse PDF without block creation.<br><br>

<b>Service:</b> Docling Service<br>
<b>Port:</b> 8081<br>
<b>Base URL:</b> <code>http://localhost:8081</code><br><br>

<b>Authentication:</b> Internal only - called by Indexing Service<br><br>

<b>Note:</b> This endpoint only parses the PDF structure without making
LLM calls for table processing. Use <code>/create-blocks</code> for Phase 2.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="doclingParsePdf" method="post" path="/docling/parse-pdf" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
});

async function run() {
  const result = await pipeshub.doclingService.parsePdf({
    recordName: "<value>",
    pdfBinary: "<value>",
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { doclingServiceParsePdf } from "pipeshub/funcs/docling-service-parse-pdf.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
});

async function run() {
  const res = await doclingServiceParsePdf(pipeshub, {
    recordName: "<value>",
    pdfBinary: "<value>",
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("doclingServiceParsePdf failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.DoclingParsePdfRequest](../../models/operations/docling-parse-pdf-request.md)                                                                                      | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |
| `options.serverURL`                                                                                                                                                            | *string*                                                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                             | An optional server URL to use.                                                                                                                                                 |

### Response

**Promise\<[operations.DoclingParsePdfResponse](../../models/operations/docling-parse-pdf-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## createBlocks

⚠️ <b>INTERNAL SERVICE ENDPOINT</b><br><br>

Phase 2 of two-phase PDF processing - create blocks from parse result.<br><br>

<b>Service:</b> Docling Service<br>
<b>Port:</b> 8081<br>
<b>Base URL:</b> <code>http://localhost:8081</code><br><br>

<b>Authentication:</b> Internal only - called by Indexing Service<br><br>

<b>Note:</b> This endpoint creates content blocks from a previously parsed
PDF document. It may involve LLM calls for table processing.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="doclingCreateBlocks" method="post" path="/docling/create-blocks" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
});

async function run() {
  const result = await pipeshub.doclingService.createBlocks({
    parseResult: "<value>",
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { doclingServiceCreateBlocks } from "pipeshub/funcs/docling-service-create-blocks.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
});

async function run() {
  const res = await doclingServiceCreateBlocks(pipeshub, {
    parseResult: "<value>",
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("doclingServiceCreateBlocks failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.DoclingCreateBlocksRequest](../../models/operations/docling-create-blocks-request.md)                                                                              | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |
| `options.serverURL`                                                                                                                                                            | *string*                                                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                             | An optional server URL to use.                                                                                                                                                 |

### Response

**Promise\<[operations.DoclingCreateBlocksResponse](../../models/operations/docling-create-blocks-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |