# RollBackToPreviousVersionRequest

## Example Usage

```typescript
import { RollBackToPreviousVersionRequest } from "pipeshub/models/operations";

let value: RollBackToPreviousVersionRequest = {
  documentId: "507f1f77bcf86cd799439011",
  body: {
    version: "2",
    note: "Reverting to version 2 due to incorrect data in version 3",
  },
};
```

## Fields

| Field                                                                                                                    | Type                                                                                                                     | Required                                                                                                                 | Description                                                                                                              | Example                                                                                                                  |
| ------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------ |
| `documentId`                                                                                                             | *string*                                                                                                                 | :heavy_check_mark:                                                                                                       | Document ID (24-character MongoDB ObjectId)                                                                              | 507f1f77bcf86cd799439011                                                                                                 |
| `body`                                                                                                                   | [operations.RollBackToPreviousVersionRequestBody](../../models/operations/roll-back-to-previous-version-request-body.md) | :heavy_check_mark:                                                                                                       | Request payload                                                                                                          |                                                                                                                          |