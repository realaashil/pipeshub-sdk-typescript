# UnshareConversationRequestBody

Request payload

## Example Usage

```typescript
import { UnshareConversationRequestBody } from "pipeshub/models/operations";

let value: UnshareConversationRequestBody = {
  userIds: [
    "<value 1>",
    "<value 2>",
    "<value 3>",
  ],
};
```

## Fields

| Field                          | Type                           | Required                       | Description                    |
| ------------------------------ | ------------------------------ | ------------------------------ | ------------------------------ |
| `userIds`                      | *string*[]                     | :heavy_check_mark:             | User IDs to remove access from |