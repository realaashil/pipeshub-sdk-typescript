# QueryServiceChatRequest

Request payload

## Example Usage

```typescript
import { QueryServiceChatRequest } from "pipeshub/models/operations";

let value: QueryServiceChatRequest = {
  query: "<value>",
};
```

## Fields

| Field                                                                                       | Type                                                                                        | Required                                                                                    | Description                                                                                 |
| ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| `query`                                                                                     | *string*                                                                                    | :heavy_check_mark:                                                                          | User's question                                                                             |
| `limit`                                                                                     | *number*                                                                                    | :heavy_minus_sign:                                                                          | N/A                                                                                         |
| `previousConversations`                                                                     | [operations.PreviousConversation](../../models/operations/previous-conversation.md)[]       | :heavy_minus_sign:                                                                          | N/A                                                                                         |
| `filters`                                                                                   | [operations.QueryServiceChatFilters](../../models/operations/query-service-chat-filters.md) | :heavy_minus_sign:                                                                          | N/A                                                                                         |
| `retrievalMode`                                                                             | [operations.RetrievalMode](../../models/operations/retrieval-mode.md)                       | :heavy_minus_sign:                                                                          | N/A                                                                                         |
| `quickMode`                                                                                 | *boolean*                                                                                   | :heavy_minus_sign:                                                                          | N/A                                                                                         |
| `modelKey`                                                                                  | *string*                                                                                    | :heavy_minus_sign:                                                                          | UUID of the model configuration                                                             |
| `modelName`                                                                                 | *string*                                                                                    | :heavy_minus_sign:                                                                          | Model name (e.g., gpt-4o-mini, claude-3-5-sonnet)                                           |
| `chatMode`                                                                                  | [operations.ChatMode](../../models/operations/chat-mode.md)                                 | :heavy_minus_sign:                                                                          | N/A                                                                                         |