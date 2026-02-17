# DocumentS3

S3-specific storage information (if storageVendor is s3)

## Example Usage

```typescript
import { DocumentS3 } from "pipeshub/models";

let value: DocumentS3 = {
  url: "s3://bucket-name/path/to/file.pdf",
};
```

## Fields

| Field                             | Type                              | Required                          | Description                       | Example                           |
| --------------------------------- | --------------------------------- | --------------------------------- | --------------------------------- | --------------------------------- |
| `url`                             | *string*                          | :heavy_minus_sign:                | S3 object URL                     | s3://bucket-name/path/to/file.pdf |