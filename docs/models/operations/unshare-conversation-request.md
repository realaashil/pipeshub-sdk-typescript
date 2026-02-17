# UnshareConversationRequest

## Example Usage

```typescript
import { UnshareConversationRequest } from "pipeshub/models/operations";

let value: UnshareConversationRequest = {
  conversationId: "<value>",
  body: {
    userIds: [
      "<value 1>",
      "<value 2>",
      "<value 3>",
    ],
  },
};
```

## Fields

| Field                                                                                                     | Type                                                                                                      | Required                                                                                                  | Description                                                                                               |
| --------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| `conversationId`                                                                                          | *string*                                                                                                  | :heavy_check_mark:                                                                                        | N/A                                                                                                       |
| `body`                                                                                                    | [operations.UnshareConversationRequestBody](../../models/operations/unshare-conversation-request-body.md) | :heavy_check_mark:                                                                                        | Request payload                                                                                           |