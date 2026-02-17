# UploadNextVersionResponse

New version uploaded successfully

## Example Usage

```typescript
import { UploadNextVersionResponse } from "pipeshub/models/operations";

let value: UploadNextVersionResponse = {
  success: true,
  message: "Version 3 uploaded successfully",
  data: {
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
  },
};
```

## Fields

| Field                                                                                                                                                                                     | Type                                                                                                                                                                                      | Required                                                                                                                                                                                  | Description                                                                                                                                                                               | Example                                                                                                                                                                                   |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `success`                                                                                                                                                                                 | *boolean*                                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                                        | N/A                                                                                                                                                                                       | true                                                                                                                                                                                      |
| `message`                                                                                                                                                                                 | *string*                                                                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                                        | N/A                                                                                                                                                                                       | Version 3 uploaded successfully                                                                                                                                                           |
| `data`                                                                                                                                                                                    | [models.Document](../../models/document.md)                                                                                                                                               | :heavy_minus_sign:                                                                                                                                                                        | Represents a document stored in PipesHub storage system. Documents can be versioned to maintain complete history of changes. Supports multiple storage backends (S3, Azure Blob, Local).<br/> |                                                                                                                                                                                           |