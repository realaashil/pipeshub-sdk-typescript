# GetUserGroupStatsData

## Example Usage

```typescript
import { GetUserGroupStatsData } from "pipeshub/models/operations";

let value: GetUserGroupStatsData = {
  totalGroups: 12,
  groupsByType: {
    admin: 1,
    standard: 5,
    everyone: 1,
    custom: 5,
  },
  totalMembers: 156,
};
```

## Fields

| Field                                                                                        | Type                                                                                         | Required                                                                                     | Description                                                                                  | Example                                                                                      |
| -------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| `totalGroups`                                                                                | *number*                                                                                     | :heavy_minus_sign:                                                                           | N/A                                                                                          | 12                                                                                           |
| `groupsByType`                                                                               | [operations.GroupsByType](../../models/operations/groups-by-type.md)                         | :heavy_minus_sign:                                                                           | N/A                                                                                          |                                                                                              |
| `totalMembers`                                                                               | *number*                                                                                     | :heavy_minus_sign:                                                                           | Sum of all group memberships (may include duplicates)                                        | 156                                                                                          |
| `groups`                                                                                     | [operations.GetUserGroupStatsGroup](../../models/operations/get-user-group-stats-group.md)[] | :heavy_minus_sign:                                                                           | N/A                                                                                          |                                                                                              |