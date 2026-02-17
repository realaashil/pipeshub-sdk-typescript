# RemoveUsersFromTeamResponse

Users removed from team successfully

## Example Usage

```typescript
import { RemoveUsersFromTeamResponse } from "pipeshub/models/operations";

let value: RemoveUsersFromTeamResponse = {
  success: true,
  message: "1 user removed from team",
  removedCount: 1,
};
```

## Fields

| Field                    | Type                     | Required                 | Description              | Example                  |
| ------------------------ | ------------------------ | ------------------------ | ------------------------ | ------------------------ |
| `success`                | *boolean*                | :heavy_minus_sign:       | N/A                      | true                     |
| `message`                | *string*                 | :heavy_minus_sign:       | N/A                      | 1 user removed from team |
| `removedCount`           | *number*                 | :heavy_minus_sign:       | N/A                      | 1                        |