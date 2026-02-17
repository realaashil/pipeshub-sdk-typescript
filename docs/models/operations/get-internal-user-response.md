# GetInternalUserResponse

User retrieved successfully

## Example Usage

```typescript
import { GetInternalUserResponse } from "pipeshub/models/operations";

let value: GetInternalUserResponse = {
  success: true,
};
```

## Fields

| Field                               | Type                                | Required                            | Description                         | Example                             |
| ----------------------------------- | ----------------------------------- | ----------------------------------- | ----------------------------------- | ----------------------------------- |
| `success`                           | *boolean*                           | :heavy_minus_sign:                  | N/A                                 | true                                |
| `data`                              | [models.User](../../models/user.md) | :heavy_minus_sign:                  | User account in an organization     |                                     |