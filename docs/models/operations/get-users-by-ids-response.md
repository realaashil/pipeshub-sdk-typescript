# GetUsersByIdsResponse

Users retrieved successfully

## Example Usage

```typescript
import { GetUsersByIdsResponse } from "pipeshub/models/operations";

let value: GetUsersByIdsResponse = {
  success: true,
};
```

## Fields

| Field                                 | Type                                  | Required                              | Description                           | Example                               |
| ------------------------------------- | ------------------------------------- | ------------------------------------- | ------------------------------------- | ------------------------------------- |
| `success`                             | *boolean*                             | :heavy_minus_sign:                    | N/A                                   | true                                  |
| `data`                                | [models.User](../../models/user.md)[] | :heavy_minus_sign:                    | N/A                                   |                                       |
| `requestedCount`                      | *number*                              | :heavy_minus_sign:                    | Number of IDs requested               |                                       |
| `foundCount`                          | *number*                              | :heavy_minus_sign:                    | Number of users found                 |                                       |