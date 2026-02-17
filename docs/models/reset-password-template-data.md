# ResetPasswordTemplateData

Template data for password reset email

## Example Usage

```typescript
import { ResetPasswordTemplateData } from "pipeshub/models";

let value: ResetPasswordTemplateData = {
  name: "John Doe",
  link: "https://app.pipeshub.com/reset-password?token=abc123xyz",
};
```

## Fields

| Field                                                   | Type                                                    | Required                                                | Description                                             | Example                                                 |
| ------------------------------------------------------- | ------------------------------------------------------- | ------------------------------------------------------- | ------------------------------------------------------- | ------------------------------------------------------- |
| `name`                                                  | *string*                                                | :heavy_check_mark:                                      | User's display name shown in the email greeting         | John Doe                                                |
| `link`                                                  | *string*                                                | :heavy_check_mark:                                      | Password reset URL with secure token                    | https://app.pipeshub.com/reset-password?token=abc123xyz |