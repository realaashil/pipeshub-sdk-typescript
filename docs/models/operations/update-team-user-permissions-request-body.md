# UpdateTeamUserPermissionsRequestBody

Request payload

## Example Usage

```typescript
import { UpdateTeamUserPermissionsRequestBody } from "pipeshub/models/operations";

let value: UpdateTeamUserPermissionsRequestBody = {
  userId: "507f1f77bcf86cd799439012",
  role: "admin",
};
```

## Fields

| Field                                                                                                    | Type                                                                                                     | Required                                                                                                 | Description                                                                                              | Example                                                                                                  |
| -------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| `userId`                                                                                                 | *string*                                                                                                 | :heavy_check_mark:                                                                                       | ID of the user whose role to update                                                                      | 507f1f77bcf86cd799439012                                                                                 |
| `role`                                                                                                   | [operations.UpdateTeamUserPermissionsRole](../../models/operations/update-team-user-permissions-role.md) | :heavy_check_mark:                                                                                       | New role to assign to the user                                                                           | admin                                                                                                    |