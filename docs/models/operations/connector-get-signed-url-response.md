# ConnectorGetSignedUrlResponse

Signed URL generated

## Example Usage

```typescript
import { ConnectorGetSignedUrlResponse } from "pipeshub/models/operations";

let value: ConnectorGetSignedUrlResponse = {};
```

## Fields

| Field                                | Type                                 | Required                             | Description                          |
| ------------------------------------ | ------------------------------------ | ------------------------------------ | ------------------------------------ |
| `signedUrl`                          | *string*                             | :heavy_minus_sign:                   | Temporary signed URL for file access |
| `expiresAt`                          | *number*                             | :heavy_minus_sign:                   | URL expiration timestamp             |