# ConnectorReindexFailedRecordsResponse

Reindexing triggered

## Example Usage

```typescript
import { ConnectorReindexFailedRecordsResponse } from "pipeshub/models/operations";

let value: ConnectorReindexFailedRecordsResponse = {};
```

## Fields

| Field                                   | Type                                    | Required                                | Description                             |
| --------------------------------------- | --------------------------------------- | --------------------------------------- | --------------------------------------- |
| `success`                               | *boolean*                               | :heavy_minus_sign:                      | N/A                                     |
| `message`                               | *string*                                | :heavy_minus_sign:                      | N/A                                     |
| `count`                                 | *number*                                | :heavy_minus_sign:                      | Number of records queued for reindexing |