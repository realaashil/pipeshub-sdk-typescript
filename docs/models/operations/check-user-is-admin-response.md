# CheckUserIsAdminResponse

User has admin access

## Example Usage

```typescript
import { CheckUserIsAdminResponse } from "pipeshub/models/operations";

let value: CheckUserIsAdminResponse = {
  success: true,
  isAdmin: true,
  message: "User has admin access",
};
```

## Fields

| Field                                    | Type                                     | Required                                 | Description                              | Example                                  |
| ---------------------------------------- | ---------------------------------------- | ---------------------------------------- | ---------------------------------------- | ---------------------------------------- |
| `success`                                | *boolean*                                | :heavy_minus_sign:                       | N/A                                      | true                                     |
| `isAdmin`                                | *boolean*                                | :heavy_minus_sign:                       | N/A                                      | true                                     |
| `message`                                | *string*                                 | :heavy_minus_sign:                       | N/A                                      | User has admin access                    |
| `adminGroups`                            | *string*[]                               | :heavy_minus_sign:                       | List of admin groups the user belongs to |                                          |