# ResumeCrawlingJobResponse

Crawling job resumed successfully

## Example Usage

```typescript
import { ResumeCrawlingJobResponse } from "pipeshub/models/operations";

let value: ResumeCrawlingJobResponse = {
  success: true,
  message: "Crawling job resumed successfully",
  data: {
    connector: "drive",
    orgId: "507f1f77bcf86cd799439012",
    resumedAt: new Date("2024-01-15T11:00:00Z"),
  },
};
```

## Fields

| Field                                                                                   | Type                                                                                    | Required                                                                                | Description                                                                             | Example                                                                                 |
| --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| `success`                                                                               | *boolean*                                                                               | :heavy_minus_sign:                                                                      | N/A                                                                                     | true                                                                                    |
| `message`                                                                               | *string*                                                                                | :heavy_minus_sign:                                                                      | N/A                                                                                     | Crawling job resumed successfully                                                       |
| `data`                                                                                  | [operations.ResumeCrawlingJobData](../../models/operations/resume-crawling-job-data.md) | :heavy_minus_sign:                                                                      | N/A                                                                                     |                                                                                         |