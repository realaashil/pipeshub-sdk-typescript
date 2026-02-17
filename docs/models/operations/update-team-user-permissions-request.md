# UpdateTeamUserPermissionsRequest

## Example Usage

```typescript
import { UpdateTeamUserPermissionsRequest } from "pipeshub/models/operations";

let value: UpdateTeamUserPermissionsRequest = {
  teamId: "507f1f77bcf86cd799439011",
  body: {
    userId: "507f1f77bcf86cd799439012",
    role: "admin",
  },
};
```

## Fields

| Field                                                                                                                   | Type                                                                                                                    | Required                                                                                                                | Description                                                                                                             | Example                                                                                                                 |
| ----------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| `teamId`                                                                                                                | *string*                                                                                                                | :heavy_check_mark:                                                                                                      | Unique identifier of the team                                                                                           | 507f1f77bcf86cd799439011                                                                                                |
| `body`                                                                                                                  | [operations.UpdateTeamUserPermissionsRequestBody](../../models/operations/update-team-user-permissions-request-body.md) | :heavy_check_mark:                                                                                                      | Request payload                                                                                                         |                                                                                                                         |