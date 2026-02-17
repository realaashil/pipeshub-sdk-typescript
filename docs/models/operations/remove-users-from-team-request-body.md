# RemoveUsersFromTeamRequestBody

Request payload

## Example Usage

```typescript
import { RemoveUsersFromTeamRequestBody } from "pipeshub/models/operations";

let value: RemoveUsersFromTeamRequestBody = {
  userIds: [
    "507f1f77bcf86cd799439012",
  ],
};
```

## Fields

| Field                                     | Type                                      | Required                                  | Description                               | Example                                   |
| ----------------------------------------- | ----------------------------------------- | ----------------------------------------- | ----------------------------------------- | ----------------------------------------- |
| `userIds`                                 | *string*[]                                | :heavy_check_mark:                        | Array of user IDs to remove from the team | [<br/>"507f1f77bcf86cd799439012"<br/>]    |