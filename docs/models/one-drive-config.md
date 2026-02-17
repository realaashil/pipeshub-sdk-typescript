# OneDriveConfig

OneDrive/Microsoft 365 connector configuration

## Example Usage

```typescript
import { OneDriveConfig } from "pipeshub/models";

let value: OneDriveConfig = {
  clientId: "<id>",
  clientSecret: "<value>",
  tenantId: "<id>",
};
```

## Fields

| Field                                  | Type                                   | Required                               | Description                            |
| -------------------------------------- | -------------------------------------- | -------------------------------------- | -------------------------------------- |
| `clientId`                             | *string*                               | :heavy_check_mark:                     | Microsoft application client ID        |
| `clientSecret`                         | *string*                               | :heavy_check_mark:                     | Microsoft application client secret    |
| `tenantId`                             | *string*                               | :heavy_check_mark:                     | Microsoft/Azure tenant ID              |
| `hasAdminConsent`                      | *boolean*                              | :heavy_minus_sign:                     | Whether admin consent has been granted |