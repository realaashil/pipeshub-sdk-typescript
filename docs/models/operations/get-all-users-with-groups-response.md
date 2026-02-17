# GetAllUsersWithGroupsResponse

Users with groups retrieved successfully

## Example Usage

```typescript
import { GetAllUsersWithGroupsResponse } from "pipeshub/models/operations";

let value: GetAllUsersWithGroupsResponse = {
  success: true,
  data: [
    {
      id: "507f1f77bcf86cd799439011",
      fullName: "John Smith",
      groups: [
        {
          name: "Engineering Team",
        },
      ],
    },
  ],
};
```

## Fields

| Field                                                                                               | Type                                                                                                | Required                                                                                            | Description                                                                                         | Example                                                                                             |
| --------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| `success`                                                                                           | *boolean*                                                                                           | :heavy_minus_sign:                                                                                  | N/A                                                                                                 | true                                                                                                |
| `data`                                                                                              | [operations.GetAllUsersWithGroupsData](../../models/operations/get-all-users-with-groups-data.md)[] | :heavy_minus_sign:                                                                                  | N/A                                                                                                 |                                                                                                     |