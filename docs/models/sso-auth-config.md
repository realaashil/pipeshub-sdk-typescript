# SSOAuthConfig

SAML SSO authentication configuration

## Example Usage

```typescript
import { SSOAuthConfig } from "pipeshub/models";

let value: SSOAuthConfig = {
  entryPoint: "https://idp.example.com/sso/saml",
  certificate: "<value>",
  emailKey: "email",
};
```

## Fields

| Field                                                   | Type                                                    | Required                                                | Description                                             | Example                                                 |
| ------------------------------------------------------- | ------------------------------------------------------- | ------------------------------------------------------- | ------------------------------------------------------- | ------------------------------------------------------- |
| `entryPoint`                                            | *string*                                                | :heavy_check_mark:                                      | Identity provider SSO URL                               | https://idp.example.com/sso/saml                        |
| `certificate`                                           | *string*                                                | :heavy_check_mark:                                      | X.509 certificate for signature validation (PEM format) |                                                         |
| `emailKey`                                              | *string*                                                | :heavy_check_mark:                                      | SAML attribute name for user email                      | email                                                   |