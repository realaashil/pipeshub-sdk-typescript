# GetUserGroupStatsResponse

User group statistics retrieved successfully

## Example Usage

```typescript
import { GetUserGroupStatsResponse } from "pipeshub/models/operations";

let value: GetUserGroupStatsResponse = {
  success: true,
  data: {
    totalGroups: 12,
    groupsByType: {
      admin: 1,
      standard: 5,
      everyone: 1,
      custom: 5,
    },
    totalMembers: 156,
  },
};
```

## Fields

| Field                                                                                    | Type                                                                                     | Required                                                                                 | Description                                                                              | Example                                                                                  |
| ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| `success`                                                                                | *boolean*                                                                                | :heavy_minus_sign:                                                                       | N/A                                                                                      | true                                                                                     |
| `data`                                                                                   | [operations.GetUserGroupStatsData](../../models/operations/get-user-group-stats-data.md) | :heavy_minus_sign:                                                                       | N/A                                                                                      |                                                                                          |