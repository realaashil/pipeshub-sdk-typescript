# User

## Example Usage

```typescript
import { User } from "pipeshub/models/operations";

let value: User = {
  userId: "<id>",
};
```

## Fields

| Field                                                                              | Type                                                                               | Required                                                                           | Description                                                                        |
| ---------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| `userId`                                                                           | *string*                                                                           | :heavy_check_mark:                                                                 | User ID to add to the team                                                         |
| `role`                                                                             | [operations.AddUsersToTeamRole](../../models/operations/add-users-to-team-role.md) | :heavy_minus_sign:                                                                 | Role to assign to the user                                                         |