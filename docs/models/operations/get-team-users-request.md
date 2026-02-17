# GetTeamUsersRequest

## Example Usage

```typescript
import { GetTeamUsersRequest } from "pipeshub/models/operations";

let value: GetTeamUsersRequest = {
  teamId: "507f1f77bcf86cd799439011",
};
```

## Fields

| Field                                | Type                                 | Required                             | Description                          | Example                              |
| ------------------------------------ | ------------------------------------ | ------------------------------------ | ------------------------------------ | ------------------------------------ |
| `teamId`                             | *string*                             | :heavy_check_mark:                   | Unique identifier of the team        | 507f1f77bcf86cd799439011             |
| `page`                               | *number*                             | :heavy_minus_sign:                   | Page number for pagination (1-based) |                                      |
| `limit`                              | *number*                             | :heavy_minus_sign:                   | Number of users per page             |                                      |