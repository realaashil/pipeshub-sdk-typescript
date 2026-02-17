# DocumentBuffer

## Overview

### Available Operations

* [get](#get) - Get document buffer
* [update](#update) - Update document buffer

## get

Retrieve the raw binary content of a document as a buffer. Used for in-memory document processing.<br><br>
<b>Overview:</b><br>
Returns the complete file content as a binary buffer. This is useful for server-side document processing, content analysis, or format conversion.<br><br>
<b>Use Cases:</b><br>
<ul>
<li>Document parsing and text extraction</li>
<li>Format conversion pipelines</li>
<li>Content analysis and indexing</li>
<li>Thumbnail generation</li>
</ul>
<b>Version Support:</b><br>
Specify <code>version</code> to get a specific historical version's content.<br><br>
<b>Memory Considerations:</b><br>
Large files will consume significant memory. For files &gt;100MB, consider using streaming download instead.<br><br>
<b>Response Format:</b><br>
Returns Node.js Buffer object serialized as JSON with type and data array.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="getDocumentBuffer" method="get" path="/document/{documentId}/buffer" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.documentBuffer.get({
    documentId: "507f1f77bcf86cd799439011",
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { documentBufferGet } from "pipeshub/funcs/document-buffer-get.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await documentBufferGet(pipeshub, {
    documentId: "507f1f77bcf86cd799439011",
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("documentBufferGet failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.GetDocumentBufferRequest](../../models/operations/get-document-buffer-request.md)                                                                                  | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[ReadableStream<Uint8Array>](../../models/.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## update

Replace the document's file content with a new file. Updates the current version without creating version history.<br><br>
<b>Overview:</b><br>
This endpoint replaces the document's content in storage. Use this for quick updates that don't need version tracking.<br><br>
<b>When to Use:</b><br>
<ul>
<li>Updating draft documents</li>
<li>Replacing temporary files</li>
<li>Quick fixes without version history</li>
</ul>
<b>For Version Tracking:</b><br>
Use <code>/uploadNextVersion</code> instead if you need to maintain version history.<br><br>
<b>File Constraints:</b><br>
<ul>
<li>Maximum size: 100MB</li>
<li>File extension must match original document</li>
</ul>
<b>Side Effects:</b><br>
<ul>
<li>Increments <code>mutationCount</code></li>
<li>Updates <code>sizeInBytes</code></li>
<li>Updates <code>updatedAt</code> timestamp</li>
</ul>


### Example Usage

<!-- UsageSnippet language="typescript" operationID="updateDocumentBuffer" method="put" path="/document/{documentId}/buffer" -->
```typescript
import { openAsBlob } from "node:fs";
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.documentBuffer.update({
    documentId: "507f1f77bcf86cd799439011",
    body: {
      file: await openAsBlob("example.file"),
    },
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { openAsBlob } from "node:fs";
import { PipeshubCore } from "pipeshub/core.js";
import { documentBufferUpdate } from "pipeshub/funcs/document-buffer-update.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await documentBufferUpdate(pipeshub, {
    documentId: "507f1f77bcf86cd799439011",
    body: {
      file: await openAsBlob("example.file"),
    },
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("documentBufferUpdate failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.UpdateDocumentBufferRequest](../../models/operations/update-document-buffer-request.md)                                                                            | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.UpdateDocumentBufferResponse](../../models/operations/update-document-buffer-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |