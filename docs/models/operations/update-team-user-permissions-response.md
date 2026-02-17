# UpdateTeamUserPermissionsResponse

User role updated successfully

## Example Usage

```typescript
import { UpdateTeamUserPermissionsResponse } from "pipeshub/models/operations";

let value: UpdateTeamUserPermissionsResponse = {
  success: true,
  message: "User role updated to admin",
  previousRole: "member",
  newRole: "admin",
};
```

## Fields

| Field                      | Type                       | Required                   | Description                | Example                    |
| -------------------------- | -------------------------- | -------------------------- | -------------------------- | -------------------------- |
| `success`                  | *boolean*                  | :heavy_minus_sign:         | N/A                        | true                       |
| `message`                  | *string*                   | :heavy_minus_sign:         | N/A                        | User role updated to admin |
| `previousRole`             | *string*                   | :heavy_minus_sign:         | N/A                        | member                     |
| `newRole`                  | *string*                   | :heavy_minus_sign:         | N/A                        | admin                      |