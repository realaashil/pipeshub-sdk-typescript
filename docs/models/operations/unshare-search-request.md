# UnshareSearchRequest

## Example Usage

```typescript
import { UnshareSearchRequest } from "pipeshub/models/operations";

let value: UnshareSearchRequest = {
  searchId: "<value>",
  body: {
    userIds: [],
  },
};
```

## Fields

| Field                                                                                         | Type                                                                                          | Required                                                                                      | Description                                                                                   |
| --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| `searchId`                                                                                    | *string*                                                                                      | :heavy_check_mark:                                                                            | N/A                                                                                           |
| `body`                                                                                        | [operations.UnshareSearchRequestBody](../../models/operations/unshare-search-request-body.md) | :heavy_check_mark:                                                                            | Request body for Revoke search access                                                         |