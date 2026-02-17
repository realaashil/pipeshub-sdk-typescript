# GetQueueStatsResponse

Queue statistics retrieved successfully

## Example Usage

```typescript
import { GetQueueStatsResponse } from "pipeshub/models/operations";

let value: GetQueueStatsResponse = {
  success: true,
  message: "Queue statistics retrieved successfully",
  data: {
    waiting: 5,
    active: 2,
    completed: 150,
    failed: 3,
    delayed: 10,
    paused: 1,
    repeatable: 8,
    total: 171,
  },
};
```

## Fields

| Field                                            | Type                                             | Required                                         | Description                                      | Example                                          |
| ------------------------------------------------ | ------------------------------------------------ | ------------------------------------------------ | ------------------------------------------------ | ------------------------------------------------ |
| `success`                                        | *boolean*                                        | :heavy_minus_sign:                               | N/A                                              | true                                             |
| `message`                                        | *string*                                         | :heavy_minus_sign:                               | N/A                                              | Queue statistics retrieved successfully          |
| `data`                                           | [models.QueueStats](../../models/queue-stats.md) | :heavy_minus_sign:                               | Aggregate statistics for the crawling job queue  |                                                  |