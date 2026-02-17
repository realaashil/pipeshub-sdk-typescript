# GetTokenFromCodeRequest

Authorization code from Google OAuth consent

## Example Usage

```typescript
import { GetTokenFromCodeRequest } from "pipeshub/models/operations";

let value: GetTokenFromCodeRequest = {
  code: "<value>",
};
```

## Fields

| Field                                             | Type                                              | Required                                          | Description                                       |
| ------------------------------------------------- | ------------------------------------------------- | ------------------------------------------------- | ------------------------------------------------- |
| `code`                                            | *string*                                          | :heavy_check_mark:                                | Authorization code from Google OAuth consent flow |