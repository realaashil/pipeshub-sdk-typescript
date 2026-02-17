# UpdateSamlAppConfigResponse

Configuration reloaded successfully

## Example Usage

```typescript
import { UpdateSamlAppConfigResponse } from "pipeshub/models/operations";

let value: UpdateSamlAppConfigResponse = {
  message: "Auth configuration updated successfully",
};
```

## Fields

| Field                                                                                            | Type                                                                                             | Required                                                                                         | Description                                                                                      | Example                                                                                          |
| ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ |
| `message`                                                                                        | *string*                                                                                         | :heavy_minus_sign:                                                                               | N/A                                                                                              | Auth configuration updated successfully                                                          |
| `config`                                                                                         | [operations.UpdateSamlAppConfigConfig](../../models/operations/update-saml-app-config-config.md) | :heavy_minus_sign:                                                                               | Updated application configuration                                                                |                                                                                                  |