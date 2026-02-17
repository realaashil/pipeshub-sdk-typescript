# ResumeCrawlingJobData

## Example Usage

```typescript
import { ResumeCrawlingJobData } from "pipeshub/models/operations";

let value: ResumeCrawlingJobData = {
  connector: "drive",
  orgId: "507f1f77bcf86cd799439012",
  resumedAt: new Date("2024-01-15T11:00:00Z"),
};
```

## Fields

| Field                                                                                         | Type                                                                                          | Required                                                                                      | Description                                                                                   | Example                                                                                       |
| --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| `connector`                                                                                   | *string*                                                                                      | :heavy_minus_sign:                                                                            | N/A                                                                                           | drive                                                                                         |
| `orgId`                                                                                       | *string*                                                                                      | :heavy_minus_sign:                                                                            | N/A                                                                                           | 507f1f77bcf86cd799439012                                                                      |
| `resumedAt`                                                                                   | [Date](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) | :heavy_minus_sign:                                                                            | N/A                                                                                           | 2024-01-15T11:00:00Z                                                                          |