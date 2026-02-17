# UpdateUserFullNameRequest

## Example Usage

```typescript
import { UpdateUserFullNameRequest } from "pipeshub/models/operations";

let value: UpdateUserFullNameRequest = {
  id: "<id>",
  body: {
    fullName: "Stacey Kshlerin",
  },
};
```

## Fields

| Field                                                                                                     | Type                                                                                                      | Required                                                                                                  | Description                                                                                               |
| --------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| `id`                                                                                                      | *string*                                                                                                  | :heavy_check_mark:                                                                                        | N/A                                                                                                       |
| `body`                                                                                                    | [operations.UpdateUserFullNameRequestBody](../../models/operations/update-user-full-name-request-body.md) | :heavy_check_mark:                                                                                        | Request payload                                                                                           |