# AtlassianConfig

Atlassian (Confluence/Jira) OAuth configuration

## Example Usage

```typescript
import { AtlassianConfig } from "pipeshub/models";

let value: AtlassianConfig = {
  clientId: "<id>",
  clientSecret: "<value>",
};
```

## Fields

| Field                         | Type                          | Required                      | Description                   |
| ----------------------------- | ----------------------------- | ----------------------------- | ----------------------------- |
| `clientId`                    | *string*                      | :heavy_check_mark:            | Atlassian OAuth client ID     |
| `clientSecret`                | *string*                      | :heavy_check_mark:            | Atlassian OAuth client secret |