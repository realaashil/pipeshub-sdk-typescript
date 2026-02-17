# DocumentAzureBlob

Azure Blob-specific storage information (if storageVendor is azureBlob)

## Example Usage

```typescript
import { DocumentAzureBlob } from "pipeshub/models";

let value: DocumentAzureBlob = {
  url: "https://account.blob.core.windows.net/container/path/file.pdf",
};
```

## Fields

| Field                                                         | Type                                                          | Required                                                      | Description                                                   | Example                                                       |
| ------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- |
| `url`                                                         | *string*                                                      | :heavy_minus_sign:                                            | Azure Blob URL                                                | https://account.blob.core.windows.net/container/path/file.pdf |