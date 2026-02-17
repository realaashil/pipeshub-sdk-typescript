# GetDirectUploadUrlResponse

Direct upload URL generated successfully

## Example Usage

```typescript
import { GetDirectUploadUrlResponse } from "pipeshub/models/operations";

let value: GetDirectUploadUrlResponse = {
  success: true,
  signedUrl:
    "https://bucket.s3.amazonaws.com/path/file.pdf?X-Amz-Signature=...",
  documentId: "507f1f77bcf86cd799439011",
};
```

## Fields

| Field                                                             | Type                                                              | Required                                                          | Description                                                       | Example                                                           |
| ----------------------------------------------------------------- | ----------------------------------------------------------------- | ----------------------------------------------------------------- | ----------------------------------------------------------------- | ----------------------------------------------------------------- |
| `success`                                                         | *boolean*                                                         | :heavy_minus_sign:                                                | N/A                                                               | true                                                              |
| `signedUrl`                                                       | *string*                                                          | :heavy_minus_sign:                                                | Presigned URL for direct PUT upload                               | https://bucket.s3.amazonaws.com/path/file.pdf?X-Amz-Signature=... |
| `documentId`                                                      | *string*                                                          | :heavy_minus_sign:                                                | Document ID for reference                                         | 507f1f77bcf86cd799439011                                          |