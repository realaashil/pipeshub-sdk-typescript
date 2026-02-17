# GoogleWorkspaceOAuthConfig

Google Workspace OAuth configuration for connectors

## Example Usage

```typescript
import { GoogleWorkspaceOAuthConfig } from "pipeshub/models";

let value: GoogleWorkspaceOAuthConfig = {
  clientId: "<id>",
  clientSecret: "<value>",
};
```

## Fields

| Field                                                                 | Type                                                                  | Required                                                              | Description                                                           |
| --------------------------------------------------------------------- | --------------------------------------------------------------------- | --------------------------------------------------------------------- | --------------------------------------------------------------------- |
| `clientId`                                                            | *string*                                                              | :heavy_check_mark:                                                    | Google OAuth client ID                                                |
| `clientSecret`                                                        | *string*                                                              | :heavy_check_mark:                                                    | Google OAuth client secret                                            |
| `enableRealTimeUpdates`                                               | *boolean*                                                             | :heavy_minus_sign:                                                    | Enable Google Pub/Sub for real-time updates                           |
| `topicName`                                                           | *string*                                                              | :heavy_minus_sign:                                                    | Google Pub/Sub topic name (required if enableRealTimeUpdates is true) |