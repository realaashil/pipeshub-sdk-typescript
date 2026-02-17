# UploadRecordsToFolderRequestBody

Request payload

## Example Usage

```typescript
import { openAsBlob } from "node:fs";
import { UploadRecordsToFolderRequestBody } from "pipeshub/models/operations";

let value: UploadRecordsToFolderRequestBody = {
  files: [
    await openAsBlob("example.file"),
  ],
};
```

## Fields

| Field                                                                                              | Type                                                                                               | Required                                                                                           | Description                                                                                        |
| -------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| `files`                                                                                            | [operations.UploadRecordsToFolderFile](../../models/operations/upload-records-to-folder-file.md)[] | :heavy_check_mark:                                                                                 | N/A                                                                                                |
| `filesMetadata`                                                                                    | *string*                                                                                           | :heavy_minus_sign:                                                                                 | JSON array with file metadata                                                                      |
| `isVersioned`                                                                                      | *boolean*                                                                                          | :heavy_minus_sign:                                                                                 | N/A                                                                                                |