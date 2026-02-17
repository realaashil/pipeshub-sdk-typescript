# CheckUserExistsByEmailResponse

Email check completed

## Example Usage

```typescript
import { CheckUserExistsByEmailResponse } from "pipeshub/models/operations";

let value: CheckUserExistsByEmailResponse = {
  success: true,
};
```

## Fields

| Field                                 | Type                                  | Required                              | Description                           | Example                               |
| ------------------------------------- | ------------------------------------- | ------------------------------------- | ------------------------------------- | ------------------------------------- |
| `success`                             | *boolean*                             | :heavy_minus_sign:                    | N/A                                   | true                                  |
| `exists`                              | *boolean*                             | :heavy_minus_sign:                    | Whether a user exists with this email |                                       |
| `data`                                | [models.User](../../models/user.md)[] | :heavy_minus_sign:                    | N/A                                   |                                       |