# AddUsersToTeamRequest

## Example Usage

```typescript
import { AddUsersToTeamRequest } from "pipeshub/models/operations";

let value: AddUsersToTeamRequest = {
  teamId: "507f1f77bcf86cd799439011",
  body: {
    users: [
      {
        userId: "507f1f77bcf86cd799439012",
      },
      {
        userId: "507f1f77bcf86cd799439013",
        role: "admin",
      },
    ],
  },
};
```

## Fields

| Field                                                                                             | Type                                                                                              | Required                                                                                          | Description                                                                                       | Example                                                                                           |
| ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| `teamId`                                                                                          | *string*                                                                                          | :heavy_check_mark:                                                                                | Unique identifier of the team                                                                     | 507f1f77bcf86cd799439011                                                                          |
| `body`                                                                                            | [operations.AddUsersToTeamRequestBody](../../models/operations/add-users-to-team-request-body.md) | :heavy_check_mark:                                                                                | Request payload                                                                                   |                                                                                                   |