# SharePointConfig

SharePoint connector configuration

## Example Usage

```typescript
import { SharePointConfig } from "pipeshub/models";

let value: SharePointConfig = {
  clientId: "<id>",
  clientSecret: "<value>",
  tenantId: "<id>",
  sharepointDomain: "<value>",
};
```

## Fields

| Field                                                | Type                                                 | Required                                             | Description                                          |
| ---------------------------------------------------- | ---------------------------------------------------- | ---------------------------------------------------- | ---------------------------------------------------- |
| `clientId`                                           | *string*                                             | :heavy_check_mark:                                   | Microsoft application client ID                      |
| `clientSecret`                                       | *string*                                             | :heavy_check_mark:                                   | Microsoft application client secret                  |
| `tenantId`                                           | *string*                                             | :heavy_check_mark:                                   | Microsoft/Azure tenant ID                            |
| `sharepointDomain`                                   | *string*                                             | :heavy_check_mark:                                   | SharePoint domain (e.g., 'mycompany.sharepoint.com') |
| `hasAdminConsent`                                    | *boolean*                                            | :heavy_minus_sign:                                   | Whether admin consent has been granted               |