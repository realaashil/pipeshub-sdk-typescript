# DocumentLocal

Local storage-specific information (if storageVendor is local)

## Example Usage

```typescript
import { DocumentLocal } from "pipeshub/models";

let value: DocumentLocal = {};
```

## Fields

| Field                       | Type                        | Required                    | Description                 |
| --------------------------- | --------------------------- | --------------------------- | --------------------------- |
| `url`                       | *string*                    | :heavy_minus_sign:          | Local file path             |
| `localPath`                 | *string*                    | :heavy_minus_sign:          | Absolute path on filesystem |