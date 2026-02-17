# MoveRecordRequestBody

Target parent folder for the record

## Example Usage

```typescript
import { MoveRecordRequestBody } from "pipeshub/models/operations";

let value: MoveRecordRequestBody = {
  newParentId: "<id>",
};
```

## Fields

| Field                                                      | Type                                                       | Required                                                   | Description                                                |
| ---------------------------------------------------------- | ---------------------------------------------------------- | ---------------------------------------------------------- | ---------------------------------------------------------- |
| `newParentId`                                              | *string*                                                   | :heavy_check_mark:                                         | ID of the new parent folder, or null to move to root level |