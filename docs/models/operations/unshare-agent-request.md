# UnshareAgentRequest

## Example Usage

```typescript
import { UnshareAgentRequest } from "pipeshub/models/operations";

let value: UnshareAgentRequest = {
  agentKey: "<value>",
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

| Field                                                                                       | Type                                                                                        | Required                                                                                    | Description                                                                                 |
| ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| `agentKey`                                                                                  | *string*                                                                                    | :heavy_check_mark:                                                                          | N/A                                                                                         |
| `body`                                                                                      | [operations.UnshareAgentRequestBody](../../models/operations/unshare-agent-request-body.md) | :heavy_check_mark:                                                                          | Request body for Revoke agent access                                                        |