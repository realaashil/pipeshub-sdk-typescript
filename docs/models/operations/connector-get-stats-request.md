# ConnectorGetStatsRequest

## Example Usage

```typescript
import { ConnectorGetStatsRequest } from "pipeshub/models/operations";

let value: ConnectorGetStatsRequest = {
  orgId: "<id>",
  connector: "<value>",
};
```

## Fields

| Field                                         | Type                                          | Required                                      | Description                                   |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| `orgId`                                       | *string*                                      | :heavy_check_mark:                            | Organization ID                               |
| `connector`                                   | *string*                                      | :heavy_check_mark:                            | Connector name (e.g., GOOGLE_DRIVE, ONEDRIVE) |