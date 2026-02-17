# UpdateSmtpConfigResponse

SMTP configuration reloaded successfully

## Example Usage

```typescript
import { UpdateSmtpConfigResponse } from "pipeshub/models/operations";

let value: UpdateSmtpConfigResponse = {
  message: "SMTP configuration updated successfully",
  smtp: {
    host: "smtp.gmail.com",
    port: 587,
    username: "notifications@yourcompany.com",
    password: "your-app-password",
    fromEmail: "noreply@yourcompany.com",
  },
};
```

## Fields

| Field                                                                                                   | Type                                                                                                    | Required                                                                                                | Description                                                                                             | Example                                                                                                 |
| ------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| `message`                                                                                               | *string*                                                                                                | :heavy_minus_sign:                                                                                      | Success message                                                                                         | SMTP configuration updated successfully                                                                 |
| `smtp`                                                                                                  | [models.SMTPConfig](../../models/smtp-config.md)                                                        | :heavy_minus_sign:                                                                                      | SMTP email server configuration for sending system emails (invitations, notifications, password resets) |                                                                                                         |