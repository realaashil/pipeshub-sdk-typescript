# GetAllUsersWithGroupsData

## Example Usage

```typescript
import { GetAllUsersWithGroupsData } from "pipeshub/models/operations";

let value: GetAllUsersWithGroupsData = {
  id: "507f1f77bcf86cd799439011",
  fullName: "John Smith",
  groups: [
    {
      name: "Engineering Team",
    },
  ],
};
```

## Fields

| Field                                                                                                 | Type                                                                                                  | Required                                                                                              | Description                                                                                           | Example                                                                                               |
| ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| `id`                                                                                                  | *string*                                                                                              | :heavy_minus_sign:                                                                                    | N/A                                                                                                   | 507f1f77bcf86cd799439011                                                                              |
| `userId`                                                                                              | *string*                                                                                              | :heavy_minus_sign:                                                                                    | N/A                                                                                                   |                                                                                                       |
| `orgId`                                                                                               | *string*                                                                                              | :heavy_minus_sign:                                                                                    | N/A                                                                                                   |                                                                                                       |
| `fullName`                                                                                            | *string*                                                                                              | :heavy_minus_sign:                                                                                    | N/A                                                                                                   | John Smith                                                                                            |
| `hasLoggedIn`                                                                                         | *boolean*                                                                                             | :heavy_minus_sign:                                                                                    | N/A                                                                                                   |                                                                                                       |
| `groups`                                                                                              | [operations.GetAllUsersWithGroupsGroup](../../models/operations/get-all-users-with-groups-group.md)[] | :heavy_minus_sign:                                                                                    | N/A                                                                                                   |                                                                                                       |