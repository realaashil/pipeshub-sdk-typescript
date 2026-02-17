# CheckUserExistsByEmailRequest

## Example Usage

```typescript
import { CheckUserExistsByEmailRequest } from "pipeshub/models/operations";

let value: CheckUserExistsByEmailRequest = {
  email: "john.smith@company.com",
};
```

## Fields

| Field                                 | Type                                  | Required                              | Description                           | Example                               |
| ------------------------------------- | ------------------------------------- | ------------------------------------- | ------------------------------------- | ------------------------------------- |
| `email`                               | *string*                              | :heavy_check_mark:                    | Email address to check                | john.smith@company.com                |
| `includeDeleted`                      | *boolean*                             | :heavy_minus_sign:                    | Whether to include soft-deleted users |                                       |