# CheckOrgExistsResponse

Organization existence check completed

## Example Usage

```typescript
import { CheckOrgExistsResponse } from "pipeshub/models/operations";

let value: CheckOrgExistsResponse = {
  success: true,
  exists: true,
};
```

## Fields

| Field                                    | Type                                     | Required                                 | Description                              | Example                                  |
| ---------------------------------------- | ---------------------------------------- | ---------------------------------------- | ---------------------------------------- | ---------------------------------------- |
| `success`                                | *boolean*                                | :heavy_minus_sign:                       | N/A                                      | true                                     |
| `exists`                                 | *boolean*                                | :heavy_minus_sign:                       | Whether an organization has been created | true                                     |