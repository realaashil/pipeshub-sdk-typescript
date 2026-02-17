# AddUsersToTeamRequestBody

Request payload

## Example Usage

```typescript
import { AddUsersToTeamRequestBody } from "pipeshub/models/operations";

let value: AddUsersToTeamRequestBody = {
  users: [
    {
      userId: "507f1f77bcf86cd799439012",
    },
    {
      userId: "507f1f77bcf86cd799439013",
      role: "admin",
    },
  ],
};
```

## Fields

| Field                                                                                                                     | Type                                                                                                                      | Required                                                                                                                  | Description                                                                                                               | Example                                                                                                                   |
| ------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| `users`                                                                                                                   | [operations.User](../../models/operations/user.md)[]                                                                      | :heavy_check_mark:                                                                                                        | N/A                                                                                                                       | [<br/>{<br/>"userId": "507f1f77bcf86cd799439012",<br/>"role": "member"<br/>},<br/>{<br/>"userId": "507f1f77bcf86cd799439013",<br/>"role": "admin"<br/>}<br/>] |