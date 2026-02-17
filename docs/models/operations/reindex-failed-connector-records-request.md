# ReindexFailedConnectorRecordsRequest

Request body for Reindex failed connector records

## Example Usage

```typescript
import { ReindexFailedConnectorRecordsRequest } from "pipeshub/models/operations";

let value: ReindexFailedConnectorRecordsRequest = {
  app: "GOOGLE_DRIVE",
  connectorId: "<id>",
};
```

## Fields

| Field                 | Type                  | Required              | Description           | Example               |
| --------------------- | --------------------- | --------------------- | --------------------- | --------------------- |
| `app`                 | *string*              | :heavy_check_mark:    | Connector app name    | GOOGLE_DRIVE          |
| `connectorId`         | *string*              | :heavy_check_mark:    | Connector instance ID |                       |