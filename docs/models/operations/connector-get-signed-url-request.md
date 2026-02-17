# ConnectorGetSignedUrlRequest

## Example Usage

```typescript
import { ConnectorGetSignedUrlRequest } from "pipeshub/models/operations";

let value: ConnectorGetSignedUrlRequest = {
  orgId: "<id>",
  userId: "<id>",
  connector: "<value>",
  recordId: "<id>",
};
```

## Fields

| Field              | Type               | Required           | Description        |
| ------------------ | ------------------ | ------------------ | ------------------ |
| `orgId`            | *string*           | :heavy_check_mark: | Organization ID    |
| `userId`           | *string*           | :heavy_check_mark: | User ID            |
| `connector`        | *string*           | :heavy_check_mark: | Connector name     |
| `recordId`         | *string*           | :heavy_check_mark: | Record ID          |