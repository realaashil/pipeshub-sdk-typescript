# Document

Represents a document stored in PipesHub storage system. Documents can be versioned to maintain complete history of changes. Supports multiple storage backends (S3, Azure Blob, Local).


## Example Usage

```typescript
import { Document } from "pipeshub/models";

let value: Document = {
  id: "507f1f77bcf86cd799439011",
  documentName: "Q4 Financial Report.pdf",
  alternateDocumentName: "2024-Q4-Finance",
  documentPath: "/reports/finance/2024",
  isVersionedFile: true,
  orgId: "507f1f77bcf86cd799439012",
  permissions: "owner",
  initiatorUserId: "507f1f77bcf86cd799439013",
  sizeInBytes: 1048576,
  mimeType: "application/pdf",
  extension: ".pdf",
  mutationCount: 5,
  versionHistory: [
    {
      version: 2,
      userAssignedVersionLabel: "v1.2",
      note: "Added executive summary section",
      extension: ".pdf",
      size: 1048576,
      mutationCount: 3,
      createdAt: 1704153600000,
      initiatedByUserId: "507f1f77bcf86cd799439013",
    },
  ],
  tags: [
    "finance",
    "quarterly",
    "report",
  ],
  storageVendor: "s3",
  s3: {
    url: "s3://bucket-name/path/to/file.pdf",
  },
  azureBlob: {
    url: "https://account.blob.core.windows.net/container/path/file.pdf",
  },
  createdAt: 1704067200000,
  updatedAt: 1704153600000,
};
```

## Fields

| Field                                                                   | Type                                                                    | Required                                                                | Description                                                             | Example                                                                 |
| ----------------------------------------------------------------------- | ----------------------------------------------------------------------- | ----------------------------------------------------------------------- | ----------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| `id`                                                                    | *string*                                                                | :heavy_check_mark:                                                      | Document unique identifier (MongoDB ObjectId)                           | 507f1f77bcf86cd799439011                                                |
| `documentName`                                                          | *string*                                                                | :heavy_check_mark:                                                      | Display name of the document                                            | Q4 Financial Report.pdf                                                 |
| `alternateDocumentName`                                                 | *string*                                                                | :heavy_minus_sign:                                                      | Alternative name for search/display purposes                            | 2024-Q4-Finance                                                         |
| `documentPath`                                                          | *string*                                                                | :heavy_minus_sign:                                                      | Virtual folder path for organization                                    | /reports/finance/2024                                                   |
| `isVersionedFile`                                                       | *boolean*                                                               | :heavy_check_mark:                                                      | Whether version control is enabled for this document                    | true                                                                    |
| `orgId`                                                                 | *string*                                                                | :heavy_check_mark:                                                      | Organization ID the document belongs to                                 | 507f1f77bcf86cd799439012                                                |
| `permissions`                                                           | [models.Permissions](../models/permissions.md)                          | :heavy_minus_sign:                                                      | Default permission level for shared access                              | owner                                                                   |
| `initiatorUserId`                                                       | *string*                                                                | :heavy_minus_sign:                                                      | User ID who created/uploaded the document                               | 507f1f77bcf86cd799439013                                                |
| `sizeInBytes`                                                           | *number*                                                                | :heavy_minus_sign:                                                      | File size in bytes                                                      | 1048576                                                                 |
| `mimeType`                                                              | *string*                                                                | :heavy_minus_sign:                                                      | MIME type of the document                                               | application/pdf                                                         |
| `extension`                                                             | *string*                                                                | :heavy_minus_sign:                                                      | File extension (with leading dot)                                       | .pdf                                                                    |
| `mutationCount`                                                         | *number*                                                                | :heavy_minus_sign:                                                      | Number of times the document has been updated                           | 5                                                                       |
| `versionHistory`                                                        | [models.DocumentVersion](../models/document-version.md)[]               | :heavy_minus_sign:                                                      | Complete version history (for versioned documents)                      |                                                                         |
| `customMetadata`                                                        | [models.CustomMetadatum](../models/custom-metadatum.md)[]               | :heavy_minus_sign:                                                      | Custom key-value metadata pairs                                         |                                                                         |
| `tags`                                                                  | *string*[]                                                              | :heavy_minus_sign:                                                      | Tags for categorization and search                                      | [<br/>"finance",<br/>"quarterly",<br/>"report"<br/>]                    |
| `storageVendor`                                                         | [models.StorageVendor](../models/storage-vendor.md)                     | :heavy_check_mark:                                                      | Storage backend where the file is stored                                | s3                                                                      |
| `s3`                                                                    | [models.DocumentS3](../models/document-s3.md)                           | :heavy_minus_sign:                                                      | S3-specific storage information (if storageVendor is s3)                |                                                                         |
| `azureBlob`                                                             | [models.DocumentAzureBlob](../models/document-azure-blob.md)            | :heavy_minus_sign:                                                      | Azure Blob-specific storage information (if storageVendor is azureBlob) |                                                                         |
| `local`                                                                 | [models.DocumentLocal](../models/document-local.md)                     | :heavy_minus_sign:                                                      | Local storage-specific information (if storageVendor is local)          |                                                                         |
| `createdAt`                                                             | *number*                                                                | :heavy_minus_sign:                                                      | Creation timestamp in milliseconds since epoch                          | 1704067200000                                                           |
| `updatedAt`                                                             | *number*                                                                | :heavy_minus_sign:                                                      | Last update timestamp in milliseconds since epoch                       | 1704153600000                                                           |
| `isDeleted`                                                             | *boolean*                                                               | :heavy_minus_sign:                                                      | Whether the document is soft-deleted                                    |                                                                         |
| `deletedByUserId`                                                       | *string*                                                                | :heavy_minus_sign:                                                      | User ID who deleted the document                                        |                                                                         |