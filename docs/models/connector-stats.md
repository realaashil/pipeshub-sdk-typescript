# ConnectorStats

Statistics for a connector's records

## Example Usage

```typescript
import { ConnectorStats } from "pipeshub/models";

let value: ConnectorStats = {};
```

## Fields

| Field                    | Type                     | Required                 | Description              |
| ------------------------ | ------------------------ | ------------------------ | ------------------------ |
| `connectorId`            | *string*                 | :heavy_minus_sign:       | N/A                      |
| `totalRecords`           | *number*                 | :heavy_minus_sign:       | N/A                      |
| `indexedRecords`         | *number*                 | :heavy_minus_sign:       | N/A                      |
| `failedRecords`          | *number*                 | :heavy_minus_sign:       | N/A                      |
| `pendingRecords`         | *number*                 | :heavy_minus_sign:       | N/A                      |
| `lastSyncTime`           | *number*                 | :heavy_minus_sign:       | N/A                      |
| `statusBreakdown`        | Record<string, *number*> | :heavy_minus_sign:       | N/A                      |