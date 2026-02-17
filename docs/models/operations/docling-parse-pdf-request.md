# DoclingParsePdfRequest

Request payload

## Example Usage

```typescript
import { DoclingParsePdfRequest } from "pipeshub/models/operations";

let value: DoclingParsePdfRequest = {
  recordName: "<value>",
  pdfBinary: "<value>",
};
```

## Fields

| Field                           | Type                            | Required                        | Description                     |
| ------------------------------- | ------------------------------- | ------------------------------- | ------------------------------- |
| `recordName`                    | *string*                        | :heavy_check_mark:              | Name/identifier of the document |
| `pdfBinary`                     | *string*                        | :heavy_check_mark:              | Base64 encoded PDF binary data  |