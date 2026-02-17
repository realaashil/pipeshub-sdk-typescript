# UpdateUserFirstNameRequest

## Example Usage

```typescript
import { UpdateUserFirstNameRequest } from "pipeshub/models/operations";

let value: UpdateUserFirstNameRequest = {
  id: "507f1f77bcf86cd799439011",
  body: {
    firstName: "John",
  },
};
```

## Fields

| Field                                                                                                       | Type                                                                                                        | Required                                                                                                    | Description                                                                                                 | Example                                                                                                     |
| ----------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| `id`                                                                                                        | *string*                                                                                                    | :heavy_check_mark:                                                                                          | User ID (24-character MongoDB ObjectId)                                                                     | 507f1f77bcf86cd799439011                                                                                    |
| `body`                                                                                                      | [operations.UpdateUserFirstNameRequestBody](../../models/operations/update-user-first-name-request-body.md) | :heavy_check_mark:                                                                                          | Request payload                                                                                             |                                                                                                             |