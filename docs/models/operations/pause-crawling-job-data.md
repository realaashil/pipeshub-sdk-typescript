# PauseCrawlingJobData

## Example Usage

```typescript
import { PauseCrawlingJobData } from "pipeshub/models/operations";

let value: PauseCrawlingJobData = {
  connector: "drive",
  orgId: "507f1f77bcf86cd799439012",
  pausedAt: new Date("2024-01-15T10:30:00Z"),
};
```

## Fields

| Field                                                                                         | Type                                                                                          | Required                                                                                      | Description                                                                                   | Example                                                                                       |
| --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| `connector`                                                                                   | *string*                                                                                      | :heavy_minus_sign:                                                                            | N/A                                                                                           | drive                                                                                         |
| `orgId`                                                                                       | *string*                                                                                      | :heavy_minus_sign:                                                                            | N/A                                                                                           | 507f1f77bcf86cd799439012                                                                      |
| `pausedAt`                                                                                    | [Date](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) | :heavy_minus_sign:                                                                            | N/A                                                                                           | 2024-01-15T10:30:00Z                                                                          |