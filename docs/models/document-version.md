# DocumentVersion

Represents a single version entry in a document's version history

## Example Usage

```typescript
import { DocumentVersion } from "pipeshub/models";

let value: DocumentVersion = {
  version: 2,
  userAssignedVersionLabel: "v1.2",
  note: "Added executive summary section",
  extension: ".pdf",
  size: 1048576,
  mutationCount: 3,
  createdAt: 1704153600000,
  initiatedByUserId: "507f1f77bcf86cd799439013",
};
```

## Fields

| Field                                                                       | Type                                                                        | Required                                                                    | Description                                                                 | Example                                                                     |
| --------------------------------------------------------------------------- | --------------------------------------------------------------------------- | --------------------------------------------------------------------------- | --------------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| `version`                                                                   | *number*                                                                    | :heavy_minus_sign:                                                          | Version number (0-indexed, auto-incremented)                                | 2                                                                           |
| `userAssignedVersionLabel`                                                  | *string*                                                                    | :heavy_minus_sign:                                                          | User-assigned version label (e.g., "v1.0", "Final")                         | v1.2                                                                        |
| `note`                                                                      | *string*                                                                    | :heavy_minus_sign:                                                          | Note describing this version's changes                                      | Added executive summary section                                             |
| `extension`                                                                 | *string*                                                                    | :heavy_minus_sign:                                                          | File extension for this version                                             | .pdf                                                                        |
| `size`                                                                      | *number*                                                                    | :heavy_minus_sign:                                                          | File size in bytes for this version                                         | 1048576                                                                     |
| `mutationCount`                                                             | *number*                                                                    | :heavy_minus_sign:                                                          | Mutation count at time of version creation                                  | 3                                                                           |
| `s3`                                                                        | [models.DocumentVersionS3](../models/document-version-s3.md)                | :heavy_minus_sign:                                                          | S3 storage URL for this version                                             |                                                                             |
| `azureBlob`                                                                 | [models.DocumentVersionAzureBlob](../models/document-version-azure-blob.md) | :heavy_minus_sign:                                                          | Azure Blob storage URL for this version                                     |                                                                             |
| `local`                                                                     | [models.DocumentVersionLocal](../models/document-version-local.md)          | :heavy_minus_sign:                                                          | Local storage path for this version                                         |                                                                             |
| `createdAt`                                                                 | *number*                                                                    | :heavy_minus_sign:                                                          | Version creation timestamp in milliseconds                                  | 1704153600000                                                               |
| `initiatedByUserId`                                                         | *string*                                                                    | :heavy_minus_sign:                                                          | User ID who created this version                                            | 507f1f77bcf86cd799439013                                                    |