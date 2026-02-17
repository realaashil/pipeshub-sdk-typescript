# RemoveUsersFromTeamRequest

## Example Usage

```typescript
import { RemoveUsersFromTeamRequest } from "pipeshub/models/operations";

let value: RemoveUsersFromTeamRequest = {
  teamId: "507f1f77bcf86cd799439011",
  body: {
    userIds: [
      "507f1f77bcf86cd799439012",
    ],
  },
};
```

## Fields

| Field                                                                                                       | Type                                                                                                        | Required                                                                                                    | Description                                                                                                 | Example                                                                                                     |
| ----------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| `teamId`                                                                                                    | *string*                                                                                                    | :heavy_check_mark:                                                                                          | Unique identifier of the team                                                                               | 507f1f77bcf86cd799439011                                                                                    |
| `body`                                                                                                      | [operations.RemoveUsersFromTeamRequestBody](../../models/operations/remove-users-from-team-request-body.md) | :heavy_check_mark:                                                                                          | Request payload                                                                                             |                                                                                                             |