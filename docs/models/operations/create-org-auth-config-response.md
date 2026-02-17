# CreateOrgAuthConfigResponse

Organization auth configuration created successfully

## Example Usage

```typescript
import { CreateOrgAuthConfigResponse } from "pipeshub/models/operations";

let value: CreateOrgAuthConfigResponse = {
  message: "Organization created successfully",
};
```

## Fields

| Field                             | Type                              | Required                          | Description                       | Example                           |
| --------------------------------- | --------------------------------- | --------------------------------- | --------------------------------- | --------------------------------- |
| `message`                         | *string*                          | :heavy_minus_sign:                | N/A                               | Organization created successfully |
| `orgId`                           | *string*                          | :heavy_minus_sign:                | Created organization ID           |                                   |
| `userId`                          | *string*                          | :heavy_minus_sign:                | Created admin user ID             |                                   |