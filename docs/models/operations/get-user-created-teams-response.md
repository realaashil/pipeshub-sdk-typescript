# GetUserCreatedTeamsResponse

User's created teams retrieved successfully

## Example Usage

```typescript
import { GetUserCreatedTeamsResponse } from "pipeshub/models/operations";

let value: GetUserCreatedTeamsResponse = {
  success: true,
  pagination: {
    page: 1,
    limit: 20,
    total: 3,
  },
};
```

## Fields

| Field                                                                                                    | Type                                                                                                     | Required                                                                                                 | Description                                                                                              | Example                                                                                                  |
| -------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| `success`                                                                                                | *boolean*                                                                                                | :heavy_minus_sign:                                                                                       | N/A                                                                                                      | true                                                                                                     |
| `data`                                                                                                   | [operations.GetUserCreatedTeamsData](../../models/operations/get-user-created-teams-data.md)[]           | :heavy_minus_sign:                                                                                       | N/A                                                                                                      |                                                                                                          |
| `pagination`                                                                                             | [operations.GetUserCreatedTeamsPagination](../../models/operations/get-user-created-teams-pagination.md) | :heavy_minus_sign:                                                                                       | N/A                                                                                                      |                                                                                                          |