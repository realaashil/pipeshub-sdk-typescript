# ShareSearchRequest

## Example Usage

```typescript
import { ShareSearchRequest } from "pipeshub/models/operations";

let value: ShareSearchRequest = {
  searchId: "<value>",
  body: {
    userIds: [
      "507f1f77bcf86cd799439011",
    ],
  },
};
```

## Fields

| Field                                                | Type                                                 | Required                                             | Description                                          |
| ---------------------------------------------------- | ---------------------------------------------------- | ---------------------------------------------------- | ---------------------------------------------------- |
| `searchId`                                           | *string*                                             | :heavy_check_mark:                                   | N/A                                                  |
| `body`                                               | [models.ShareRequest](../../models/share-request.md) | :heavy_check_mark:                                   | Request payload                                      |