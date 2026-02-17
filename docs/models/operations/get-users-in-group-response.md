# GetUsersInGroupResponse

Users in group retrieved successfully

## Example Usage

```typescript
import { GetUsersInGroupResponse } from "pipeshub/models/operations";

let value: GetUsersInGroupResponse = {
  success: true,
  pagination: {
    page: 1,
    limit: 20,
    total: 45,
    totalPages: 3,
  },
};
```

## Fields

| Field                                                                                            | Type                                                                                             | Required                                                                                         | Description                                                                                      | Example                                                                                          |
| ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ |
| `success`                                                                                        | *boolean*                                                                                        | :heavy_minus_sign:                                                                               | N/A                                                                                              | true                                                                                             |
| `data`                                                                                           | [models.User](../../models/user.md)[]                                                            | :heavy_minus_sign:                                                                               | N/A                                                                                              |                                                                                                  |
| `pagination`                                                                                     | [operations.GetUsersInGroupPagination](../../models/operations/get-users-in-group-pagination.md) | :heavy_minus_sign:                                                                               | N/A                                                                                              |                                                                                                  |