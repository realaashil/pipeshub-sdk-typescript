# SetMetricsPushIntervalRequest

Request payload

## Example Usage

```typescript
import { SetMetricsPushIntervalRequest } from "pipeshub/models/operations";

let value: SetMetricsPushIntervalRequest = {
  pushIntervalMs: 60000,
};
```

## Fields

| Field                                          | Type                                           | Required                                       | Description                                    | Example                                        |
| ---------------------------------------------- | ---------------------------------------------- | ---------------------------------------------- | ---------------------------------------------- | ---------------------------------------------- |
| `pushIntervalMs`                               | *number*                                       | :heavy_check_mark:                             | Push interval in milliseconds (minimum 1000ms) | 60000                                          |