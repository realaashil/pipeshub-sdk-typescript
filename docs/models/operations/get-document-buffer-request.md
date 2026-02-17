# GetDocumentBufferRequest

## Example Usage

```typescript
import { GetDocumentBufferRequest } from "pipeshub/models/operations";

let value: GetDocumentBufferRequest = {
  documentId: "507f1f77bcf86cd799439011",
};
```

## Fields

| Field                                       | Type                                        | Required                                    | Description                                 | Example                                     |
| ------------------------------------------- | ------------------------------------------- | ------------------------------------------- | ------------------------------------------- | ------------------------------------------- |
| `documentId`                                | *string*                                    | :heavy_check_mark:                          | Document ID (24-character MongoDB ObjectId) | 507f1f77bcf86cd799439011                    |
| `version`                                   | *number*                                    | :heavy_minus_sign:                          | Version number to retrieve (0-indexed)      |                                             |