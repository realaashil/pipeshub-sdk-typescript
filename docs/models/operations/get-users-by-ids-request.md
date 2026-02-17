# GetUsersByIdsRequest

Request payload

## Example Usage

```typescript
import { GetUsersByIdsRequest } from "pipeshub/models/operations";

let value: GetUsersByIdsRequest = {
  userIds: [
    "507f1f77bcf86cd799439011",
    "507f1f77bcf86cd799439012",
  ],
};
```

## Fields

| Field                                                      | Type                                                       | Required                                                   | Description                                                | Example                                                    |
| ---------------------------------------------------------- | ---------------------------------------------------------- | ---------------------------------------------------------- | ---------------------------------------------------------- | ---------------------------------------------------------- |
| `userIds`                                                  | *string*[]                                                 | :heavy_check_mark:                                         | Array of user IDs to retrieve                              | [<br/>"507f1f77bcf86cd799439011",<br/>"507f1f77bcf86cd799439012"<br/>] |