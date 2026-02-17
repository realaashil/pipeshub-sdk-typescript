# ConnectorGetStatsResponse

Connector statistics

## Example Usage

```typescript
import { ConnectorGetStatsResponse } from "pipeshub/models/operations";

let value: ConnectorGetStatsResponse = {};
```

## Fields

| Field                                  | Type                                   | Required                               | Description                            |
| -------------------------------------- | -------------------------------------- | -------------------------------------- | -------------------------------------- |
| `totalRecords`                         | *number*                               | :heavy_minus_sign:                     | Total number of records                |
| `indexedRecords`                       | *number*                               | :heavy_minus_sign:                     | Number of successfully indexed records |
| `failedRecords`                        | *number*                               | :heavy_minus_sign:                     | Number of failed records               |
| `pendingRecords`                       | *number*                               | :heavy_minus_sign:                     | Number of pending records              |
| `lastSyncTimestamp`                    | *number*                               | :heavy_minus_sign:                     | Last sync timestamp                    |