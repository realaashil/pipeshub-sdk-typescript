# CheckDocumentModifiedResponse

Modification check completed

## Example Usage

```typescript
import { CheckDocumentModifiedResponse } from "pipeshub/models/operations";

let value: CheckDocumentModifiedResponse = {
  success: true,
  isModified: true,
};
```

## Fields

| Field                                             | Type                                              | Required                                          | Description                                       | Example                                           |
| ------------------------------------------------- | ------------------------------------------------- | ------------------------------------------------- | ------------------------------------------------- | ------------------------------------------------- |
| `success`                                         | *boolean*                                         | :heavy_minus_sign:                                | N/A                                               | true                                              |
| `isModified`                                      | *boolean*                                         | :heavy_minus_sign:                                | True if current content differs from last version | true                                              |