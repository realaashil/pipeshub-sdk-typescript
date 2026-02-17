# DocumentManagement

## Overview

### Available Operations

* [getById](#getbyid) - Get document by ID
* [delete](#delete) - Delete document
* [download](#download) - Download document

## getById

Retrieve complete document metadata by its unique identifier.<br><br>
<b>Overview:</b><br>
Returns all document information including metadata, version history, storage location, and access permissions. Use this to display document details or prepare for download/edit operations.<br><br>
<b>Response Includes:</b><br>
<ul>
<li>Document metadata (name, path, size, type)</li>
<li>Storage information (vendor, URLs)</li>
<li>Version history (if versioned)</li>
<li>Permission settings</li>
<li>Custom metadata</li>
<li>Timestamps (created, updated)</li>
</ul>
<b>Authorization:</b><br>
Document must belong to the requesting user's organization.<br><br>
<b>Note:</b> Soft-deleted documents (isDeleted: true) are not returned.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="getDocumentById" method="get" path="/document/{documentId}" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.documentManagement.getById({
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
import { documentManagementGetById } from "pipeshub/funcs/document-management-get-by-id.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await documentManagementGetById(pipeshub, {
    documentId: "507f1f77bcf86cd799439011",
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("documentManagementGetById failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.GetDocumentByIdRequest](../../models/operations/get-document-by-id-request.md)                                                                                     | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.GetDocumentByIdResponse](../../models/operations/get-document-by-id-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## delete

Soft delete a document from the system. The document is marked as deleted but not permanently removed.<br><br>
<b>Overview:</b><br>
This endpoint performs a soft delete, marking the document as deleted while preserving its data for potential recovery or audit purposes.<br><br>
<b>What Happens on Delete:</b><br>
<ul>
<li><code>isDeleted</code> flag set to true</li>
<li><code>deletedByUserId</code> recorded</li>
<li>Document excluded from normal queries</li>
<li>File remains in storage (soft delete)</li>
</ul>
<b>Restrictions:</b><br>
<ul>
<li>Document must belong to user's organization</li>
<li>User must have appropriate permissions</li>
</ul>
<b>Recovery:</b><br>
Soft-deleted documents can be restored by administrators if needed.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="deleteDocumentById" method="delete" path="/document/{documentId}" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.documentManagement.delete({
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
import { documentManagementDelete } from "pipeshub/funcs/document-management-delete.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await documentManagementDelete(pipeshub, {
    documentId: "507f1f77bcf86cd799439011",
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("documentManagementDelete failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.DeleteDocumentByIdRequest](../../models/operations/delete-document-by-id-request.md)                                                                               | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.DeleteDocumentByIdResponse](../../models/operations/delete-document-by-id-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## download

Get a time-limited signed URL to download the document, or receive the file directly for local storage.<br><br>
<b>Overview:</b><br>
This endpoint generates secure download access to documents. For cloud storage (S3/Azure), it returns a presigned URL. For local storage, it streams the file directly.<br><br>
<b>Download Behavior by Storage:</b><br>
<ul>
<li><b>S3/Azure:</b> Returns presigned URL valid for specified duration</li>
<li><b>Local:</b> Streams file directly with appropriate headers</li>
</ul>
<b>Version Download:</b><br>
Specify the <code>version</code> parameter to download a specific historical version. Only available for versioned documents.<br><br>
<b>URL Expiration:</b><br>
<ul>
<li>Default: 3600 seconds (1 hour)</li>
<li>Configurable via <code>expirationTimeInSeconds</code></li>
<li>Maximum depends on storage provider limits</li>
</ul>
<b>Security:</b><br>
Signed URLs are single-use and time-limited. They can be safely shared for temporary access.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="downloadDocument" method="get" path="/document/{documentId}/download" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.documentManagement.download({
    documentId: "507f1f77bcf86cd799439011",
    version: 2,
    expirationTimeInSeconds: 7200,
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { documentManagementDownload } from "pipeshub/funcs/document-management-download.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await documentManagementDownload(pipeshub, {
    documentId: "507f1f77bcf86cd799439011",
    version: 2,
    expirationTimeInSeconds: 7200,
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("documentManagementDownload failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.DownloadDocumentRequest](../../models/operations/download-document-request.md)                                                                                     | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.DownloadDocumentResponse](../../models/operations/download-document-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |