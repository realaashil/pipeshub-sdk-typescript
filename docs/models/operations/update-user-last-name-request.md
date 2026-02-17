# UpdateUserLastNameRequest

## Example Usage

```typescript
import { UpdateUserLastNameRequest } from "pipeshub/models/operations";

let value: UpdateUserLastNameRequest = {
  id: "507f1f77bcf86cd799439011",
  body: {
    lastName: "Smith",
  },
};
```

## Fields

| Field                                                                                                     | Type                                                                                                      | Required                                                                                                  | Description                                                                                               | Example                                                                                                   |
| --------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| `id`                                                                                                      | *string*                                                                                                  | :heavy_check_mark:                                                                                        | User ID (24-character MongoDB ObjectId)                                                                   | 507f1f77bcf86cd799439011                                                                                  |
| `body`                                                                                                    | [operations.UpdateUserLastNameRequestBody](../../models/operations/update-user-last-name-request-body.md) | :heavy_check_mark:                                                                                        | Request payload                                                                                           |                                                                                                           |