# VersionControl

## Overview

### Available Operations

* [uploadNext](#uploadnext) - Upload next version
* [rollBack](#rollback) - Rollback to previous version
* [checkModified](#checkmodified) - Check if document is modified

## uploadNext

Upload a new version of a versioned document, maintaining full version history.<br><br>
<b>Overview:</b><br>
This endpoint creates a new version entry in the document's version history. The previous version remains accessible and the document can be rolled back if needed.<br><br>
<b>Version Control Flow:</b><br>
<ol>
<li>Upload new file content</li>
<li>System compares with previous version</li>
<li>If different, creates new version entry</li>
<li>Updates version history with metadata</li>
<li>Current document points to new version</li>
</ol>
<b>Version Entry Contains:</b><br>
<ul>
<li>Version number (auto-incremented)</li>
<li>Storage URL for this version</li>
<li>Size and extension</li>
<li>Optional note describing changes</li>
<li>User who created version</li>
<li>Timestamp</li>
</ul>
<b>Requirements:</b><br>
<ul>
<li>Document must have <code>isVersionedFile: true</code></li>
<li>File extension must match original document</li>
<li>Content must differ from previous version</li>
</ul>
<b>File Constraints:</b><br>
<ul>
<li>Maximum size: 100MB</li>
<li>Same extension as original required</li>
</ul>


### Example Usage

<!-- UsageSnippet language="typescript" operationID="uploadNextVersion" method="post" path="/document/{documentId}/uploadNextVersion" -->
```typescript
import { openAsBlob } from "node:fs";
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.versionControl.uploadNext({
    documentId: "507f1f77bcf86cd799439011",
    body: {
      currentVersionNote: "Draft version with initial content",
      nextVersionNote: "Final version with all revisions incorporated",
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
import { versionControlUploadNext } from "pipeshub/funcs/version-control-upload-next.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await versionControlUploadNext(pipeshub, {
    documentId: "507f1f77bcf86cd799439011",
    body: {
      currentVersionNote: "Draft version with initial content",
      nextVersionNote: "Final version with all revisions incorporated",
      file: await openAsBlob("example.file"),
    },
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("versionControlUploadNext failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.UploadNextVersionRequest](../../models/operations/upload-next-version-request.md)                                                                                  | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.UploadNextVersionResponse](../../models/operations/upload-next-version-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## rollBack

Restore a versioned document to a previous version. Creates a new version entry with the rolled-back content.<br><br>
<b>Overview:</b><br>
This endpoint allows reverting a document to any previous version while maintaining the complete version history. The rollback itself creates a new version entry.<br><br>
<b>Rollback Flow:</b><br>
<ol>
<li>Specify target version number to rollback to</li>
<li>System retrieves content from that version</li>
<li>Creates new version entry with restored content</li>
<li>Adds rollback note to version history</li>
<li>Document now shows restored content</li>
</ol>
<b>Version History Preserved:</b><br>
Rollback does NOT delete intermediate versions. Full history remains intact for audit purposes.<br><br>
<b>Requirements:</b><br>
<ul>
<li>Document must be versioned</li>
<li>Target version must exist (less than current version count)</li>
<li>Note explaining rollback reason is required</li>
</ul>
<b>Use Cases:</b><br>
<ul>
<li>Reverting accidental changes</li>
<li>Restoring to known-good state</li>
<li>Undoing problematic updates</li>
</ul>


### Example Usage

<!-- UsageSnippet language="typescript" operationID="rollBackToPreviousVersion" method="post" path="/document/{documentId}/rollBack" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.versionControl.rollBack({
    documentId: "507f1f77bcf86cd799439011",
    body: {
      version: "2",
      note: "Reverting to version 2 due to incorrect data in version 3",
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
import { versionControlRollBack } from "pipeshub/funcs/version-control-roll-back.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await versionControlRollBack(pipeshub, {
    documentId: "507f1f77bcf86cd799439011",
    body: {
      version: "2",
      note: "Reverting to version 2 due to incorrect data in version 3",
    },
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("versionControlRollBack failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.RollBackToPreviousVersionRequest](../../models/operations/roll-back-to-previous-version-request.md)                                                                | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.RollBackToPreviousVersionResponse](../../models/operations/roll-back-to-previous-version-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## checkModified

Check if the current document content differs from the last saved version. Useful for detecting unsaved changes.<br><br>
<b>Overview:</b><br>
Compares the current document buffer with the most recent version in history to detect modifications. Returns true if content has changed since last version.<br><br>
<b>Use Cases:</b><br>
<ul>
<li>Prompting user to save before closing</li>
<li>Auto-save decision making</li>
<li>Version creation validation</li>
<li>Change detection in workflows</li>
</ul>
<b>Comparison Method:</b><br>
Performs binary comparison of file buffers. Identical content returns false even if edited and reverted.<br><br>
<b>Requirements:</b><br>
Document must be versioned to have comparison baseline.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="checkDocumentModified" method="get" path="/document/{documentId}/isModified" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.versionControl.checkModified({
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
import { versionControlCheckModified } from "pipeshub/funcs/version-control-check-modified.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await versionControlCheckModified(pipeshub, {
    documentId: "507f1f77bcf86cd799439011",
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("versionControlCheckModified failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.CheckDocumentModifiedRequest](../../models/operations/check-document-modified-request.md)                                                                          | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.CheckDocumentModifiedResponse](../../models/operations/check-document-modified-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |