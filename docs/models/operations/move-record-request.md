# MoveRecordRequest

## Example Usage

```typescript
import { MoveRecordRequest } from "pipeshub/models/operations";

let value: MoveRecordRequest = {
  kbId: "87495e6e-18c0-47db-89aa-7aa1dd2e1d1c",
  recordId: "<id>",
  body: {
    newParentId: "<id>",
  },
};
```

## Fields

| Field                                                                                   | Type                                                                                    | Required                                                                                | Description                                                                             |
| --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| `kbId`                                                                                  | *string*                                                                                | :heavy_check_mark:                                                                      | Knowledge base ID                                                                       |
| `recordId`                                                                              | *string*                                                                                | :heavy_check_mark:                                                                      | Record ID to move                                                                       |
| `body`                                                                                  | [operations.MoveRecordRequestBody](../../models/operations/move-record-request-body.md) | :heavy_check_mark:                                                                      | Target parent folder for the record                                                     |