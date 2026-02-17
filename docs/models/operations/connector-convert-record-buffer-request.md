# ConnectorConvertRecordBufferRequest

Request payload

## Example Usage

```typescript
import { ConnectorConvertRecordBufferRequest } from "pipeshub/models/operations";

let value: ConnectorConvertRecordBufferRequest = {
  buffer: "<value>",
  convertTo: "<value>",
};
```

## Fields

| Field                                    | Type                                     | Required                                 | Description                              |
| ---------------------------------------- | ---------------------------------------- | ---------------------------------------- | ---------------------------------------- |
| `buffer`                                 | *string*                                 | :heavy_check_mark:                       | Base64 encoded file content              |
| `convertTo`                              | *string*                                 | :heavy_check_mark:                       | Target format (e.g., 'text', 'markdown') |
| `mimeType`                               | *string*                                 | :heavy_minus_sign:                       | Original MIME type of the file           |