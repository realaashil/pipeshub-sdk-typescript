# SetMetricsServerUrlRequest

Request payload

## Example Usage

```typescript
import { SetMetricsServerUrlRequest } from "pipeshub/models/operations";

let value: SetMetricsServerUrlRequest = {
  serverUrl: "https://metrics.mycompany.com/collect",
};
```

## Fields

| Field                                     | Type                                      | Required                                  | Description                               | Example                                   |
| ----------------------------------------- | ----------------------------------------- | ----------------------------------------- | ----------------------------------------- | ----------------------------------------- |
| `serverUrl`                               | *string*                                  | :heavy_check_mark:                        | Full URL of the metrics collection server | https://metrics.mycompany.com/collect     |