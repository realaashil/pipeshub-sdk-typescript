# GetAllUsersResponse

List of users retrieved successfully

## Example Usage

```typescript
import { GetAllUsersResponse } from "pipeshub/models/operations";

let value: GetAllUsersResponse = {
  success: true,
};
```

## Fields

| Field                                                                                   | Type                                                                                    | Required                                                                                | Description                                                                             | Example                                                                                 |
| --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| `success`                                                                               | *boolean*                                                                               | :heavy_minus_sign:                                                                      | N/A                                                                                     | true                                                                                    |
| `data`                                                                                  | [models.User](../../models/user.md)[]                                                   | :heavy_minus_sign:                                                                      | N/A                                                                                     |                                                                                         |
| `pagination`                                                                            | [operations.GetAllUsersPagination](../../models/operations/get-all-users-pagination.md) | :heavy_minus_sign:                                                                      | N/A                                                                                     |                                                                                         |