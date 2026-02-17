# DocumentUpload

## Overview

### Available Operations

* [upload](#upload) - Upload a new document
* [createPlaceholder](#createplaceholder) - Create document placeholder
* [getDirectUploadUrl](#getdirectuploadurl) - Get direct upload URL

## upload

Upload a new document to PipesHub storage. Supports multiple storage backends including S3, Azure Blob, and local storage.<br><br>
<b>Overview:</b><br>
This endpoint handles document uploads with automatic processing, metadata extraction, and optional versioning. It's the primary endpoint for adding new files to PipesHub.<br><br>
<b>Upload Flow:</b><br>
<ol>
<li>Client sends file with metadata via multipart/form-data</li>
<li>Document metadata saved to database</li>
<li>Returns document object with storage URLs</li>
</ol>
<b>File Size Limits:</b><br>
<ul>
<li><b>Maximum:</b> 1GB (1,073,741,824 bytes)</li>
<li><b>Large file threshold:</b> 10MB (triggers direct upload flow)</li>
</ul>
<b>Supported File Types:</b><br>
<ul>
<li><b>Documents:</b> PDF, DOCX, DOC, XLSX, XLS, PPTX, PPT, TXT, MD, CSV</li>
<li><b>Images:</b> PNG, JPG, JPEG, GIF, WebP, SVG, BMP, TIFF</li>
<li><b>Videos:</b> MP4, AVI, MOV, MKV, WebM</li>
<li><b>Audio:</b> MP3, WAV, FLAC, AAC</li>
<li><b>Archives:</b> ZIP, RAR, 7Z, TAR, GZ</li>
</ul>
<b>Version Control:</b><br>
Set <code>isVersionedFile: "true"</code> to enable version tracking. Versioned documents maintain full history of all changes.<br><br>
<b>Response Headers:</b><br>
<ul>
<li><code>x-document-id</code>: Unique document identifier</li>
<li><code>x-document-name</code>: Document name as stored</li>
</ul>
<b>Storage Backends:</b><br>
Automatically routes to configured storage: Amazon S3, Azure Blob Storage, or Local filesystem.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="uploadDocument" method="post" path="/document/upload" -->
```typescript
import { openAsBlob } from "node:fs";
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.documentUpload.upload({
    documentName: "Q4 Financial Report.pdf",
    documentPath: "/reports/finance/2024",
    alternateDocumentName: "2024-Q4-Finance",
    customMetadata: "{\"department\":\"finance\",\"quarter\":\"Q4\"}",
    isVersionedFile: "true",
    file: await openAsBlob("example.file"),
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
import { documentUploadUpload } from "pipeshub/funcs/document-upload-upload.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await documentUploadUpload(pipeshub, {
    documentName: "Q4 Financial Report.pdf",
    documentPath: "/reports/finance/2024",
    alternateDocumentName: "2024-Q4-Finance",
    customMetadata: "{\"department\":\"finance\",\"quarter\":\"Q4\"}",
    isVersionedFile: "true",
    file: await openAsBlob("example.file"),
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("documentUploadUpload failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.UploadDocumentRequest](../../models/operations/upload-document-request.md)                                                                                         | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.UploadDocumentResponse](../../models/operations/upload-document-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## createPlaceholder

Create a document metadata record without uploading file content. Used in conjunction with direct upload for large files.<br><br>
<b>Overview:</b><br>
This endpoint creates a document entry in the database without actual file content. The file is then uploaded directly to storage using the <code>/directUpload</code> endpoint.<br><br>
<b>Direct Upload Flow:</b><br>
<ol>
<li>Call this endpoint to create document placeholder</li>
<li>Receive document ID in response</li>
<li>Call <code>/document/{documentId}/directUpload</code> to get presigned URL</li>
<li>Upload file directly to presigned URL</li>
<li>Document becomes accessible once upload completes</li>
</ol>
<b>Use Cases:</b><br>
<ul>
<li>Large file uploads (bypassing server)</li>
<li>Client-side upload progress tracking</li>
<li>Resumable uploads</li>
<li>Reduced server memory usage</li>
</ul>
<b>Note:</b> Extension must be provided without the dot (e.g., "pdf" not ".pdf").


### Example Usage

<!-- UsageSnippet language="typescript" operationID="createDocumentPlaceholder" method="post" path="/document/placeholder" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.documentUpload.createPlaceholder({
    documentName: "Large Video File.mp4",
    documentPath: "/videos/training",
    extension: "mp4",
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { documentUploadCreatePlaceholder } from "pipeshub/funcs/document-upload-create-placeholder.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await documentUploadCreatePlaceholder(pipeshub, {
    documentName: "Large Video File.mp4",
    documentPath: "/videos/training",
    extension: "mp4",
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("documentUploadCreatePlaceholder failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.CreateDocumentPlaceholderRequest](../../models/operations/create-document-placeholder-request.md)                                                                  | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[models.Document](../../models/document.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## getDirectUploadUrl

Generate a presigned URL for direct client-to-storage upload, bypassing the server for large files.<br><br>
<b>Overview:</b><br>
This endpoint provides a presigned URL that allows clients to upload directly to storage (S3/Azure) without routing through the server. Essential for large file uploads.<br><br>
<b>Direct Upload Flow:</b><br>
<ol>
<li>Create document placeholder with <code>/placeholder</code></li>
<li>Call this endpoint with document ID</li>
<li>Receive presigned URL and document ID</li>
<li>Client uploads file directly to presigned URL (PUT request)</li>
<li>Document becomes available once upload completes</li>
</ol>
<b>Benefits:</b><br>
<ul>
<li>No server memory consumption for large files</li>
<li>Direct transfer to storage (faster)</li>
<li>Client-side progress tracking</li>
<li>Reduced server bandwidth</li>
</ul>
<b>URL Validity:</b><br>
Presigned URLs typically expire after 1 hour. Upload must complete before expiration.<br><br>
<b>Note:</b> Only available for S3 and Azure Blob storage. Local storage does not support direct upload.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="getDirectUploadUrl" method="post" path="/document/{documentId}/directUpload" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.documentUpload.getDirectUploadUrl({
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
import { documentUploadGetDirectUploadUrl } from "pipeshub/funcs/document-upload-get-direct-upload-url.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await documentUploadGetDirectUploadUrl(pipeshub, {
    documentId: "507f1f77bcf86cd799439011",
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("documentUploadGetDirectUploadUrl failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.GetDirectUploadUrlRequest](../../models/operations/get-direct-upload-url-request.md)                                                                               | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.GetDirectUploadUrlResponse](../../models/operations/get-direct-upload-url-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |