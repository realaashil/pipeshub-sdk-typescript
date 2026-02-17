# GetTeamUsersResponse

Team members retrieved successfully

## Example Usage

```typescript
import { GetTeamUsersResponse } from "pipeshub/models/operations";

let value: GetTeamUsersResponse = {
  success: true,
  pagination: {
    page: 1,
    limit: 20,
    total: 15,
  },
};
```

## Fields

| Field                                                                                     | Type                                                                                      | Required                                                                                  | Description                                                                               | Example                                                                                   |
| ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| `success`                                                                                 | *boolean*                                                                                 | :heavy_minus_sign:                                                                        | N/A                                                                                       | true                                                                                      |
| `data`                                                                                    | [operations.GetTeamUsersData](../../models/operations/get-team-users-data.md)[]           | :heavy_minus_sign:                                                                        | N/A                                                                                       |                                                                                           |
| `pagination`                                                                              | [operations.GetTeamUsersPagination](../../models/operations/get-team-users-pagination.md) | :heavy_minus_sign:                                                                        | N/A                                                                                       |                                                                                           |