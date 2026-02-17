# LoginWithOTPTemplateData

Template data for OTP login email

## Example Usage

```typescript
import { LoginWithOTPTemplateData } from "pipeshub/models";

let value: LoginWithOTPTemplateData = {
  name: "John Doe",
  otp: "123456",
};
```

## Fields

| Field                                           | Type                                            | Required                                        | Description                                     | Example                                         |
| ----------------------------------------------- | ----------------------------------------------- | ----------------------------------------------- | ----------------------------------------------- | ----------------------------------------------- |
| `name`                                          | *string*                                        | :heavy_check_mark:                              | User's display name shown in the email greeting | John Doe                                        |
| `otp`                                           | *string*                                        | :heavy_check_mark:                              | 6-digit one-time password code                  | 123456                                          |