# PauseCrawlingJobResponse

Crawling job paused successfully

## Example Usage

```typescript
import { PauseCrawlingJobResponse } from "pipeshub/models/operations";

let value: PauseCrawlingJobResponse = {
  success: true,
  message: "Crawling job paused successfully",
  data: {
    connector: "drive",
    orgId: "507f1f77bcf86cd799439012",
    pausedAt: new Date("2024-01-15T10:30:00Z"),
  },
};
```

## Fields

| Field                                                                                 | Type                                                                                  | Required                                                                              | Description                                                                           | Example                                                                               |
| ------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| `success`                                                                             | *boolean*                                                                             | :heavy_minus_sign:                                                                    | N/A                                                                                   | true                                                                                  |
| `message`                                                                             | *string*                                                                              | :heavy_minus_sign:                                                                    | N/A                                                                                   | Crawling job paused successfully                                                      |
| `data`                                                                                | [operations.PauseCrawlingJobData](../../models/operations/pause-crawling-job-data.md) | :heavy_minus_sign:                                                                    | N/A                                                                                   |                                                                                       |