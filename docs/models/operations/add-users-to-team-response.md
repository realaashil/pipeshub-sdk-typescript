# AddUsersToTeamResponse

Users added to team successfully

## Example Usage

```typescript
import { AddUsersToTeamResponse } from "pipeshub/models/operations";

let value: AddUsersToTeamResponse = {
  success: true,
  message: "2 users added to team successfully",
  addedCount: 2,
  skippedCount: 0,
};
```

## Fields

| Field                               | Type                                | Required                            | Description                         | Example                             |
| ----------------------------------- | ----------------------------------- | ----------------------------------- | ----------------------------------- | ----------------------------------- |
| `success`                           | *boolean*                           | :heavy_minus_sign:                  | N/A                                 | true                                |
| `message`                           | *string*                            | :heavy_minus_sign:                  | N/A                                 | 2 users added to team successfully  |
| `addedCount`                        | *number*                            | :heavy_minus_sign:                  | N/A                                 | 2                                   |
| `skippedCount`                      | *number*                            | :heavy_minus_sign:                  | Number of users already in the team | 0                                   |