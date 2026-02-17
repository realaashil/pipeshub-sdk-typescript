# SamlCallbackRequest

Request payload

## Example Usage

```typescript
import { SamlCallbackRequest } from "pipeshub/models/operations";

let value: SamlCallbackRequest = {
  samlResponse: "<value>",
};
```

## Fields

| Field                                          | Type                                           | Required                                       | Description                                    |
| ---------------------------------------------- | ---------------------------------------------- | ---------------------------------------------- | ---------------------------------------------- |
| `samlResponse`                                 | *string*                                       | :heavy_check_mark:                             | Base64-encoded SAML Response from IDP          |
| `relayState`                                   | *string*                                       | :heavy_minus_sign:                             | State parameter containing session information |