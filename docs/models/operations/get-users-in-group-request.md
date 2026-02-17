# GetUsersInGroupRequest

## Example Usage

```typescript
import { GetUsersInGroupRequest } from "pipeshub/models/operations";

let value: GetUsersInGroupRequest = {
  groupId: "507f1f77bcf86cd799439011",
};
```

## Fields

| Field                                | Type                                 | Required                             | Description                          | Example                              |
| ------------------------------------ | ------------------------------------ | ------------------------------------ | ------------------------------------ | ------------------------------------ |
| `groupId`                            | *string*                             | :heavy_check_mark:                   | Unique identifier of the user group  | 507f1f77bcf86cd799439011             |
| `page`                               | *number*                             | :heavy_minus_sign:                   | Page number for pagination (1-based) |                                      |
| `limit`                              | *number*                             | :heavy_minus_sign:                   | Number of users per page             |                                      |