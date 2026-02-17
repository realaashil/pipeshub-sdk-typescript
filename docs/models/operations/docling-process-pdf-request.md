# DoclingProcessPdfRequest

Request payload

## Example Usage

```typescript
import { DoclingProcessPdfRequest } from "pipeshub/models/operations";

let value: DoclingProcessPdfRequest = {
  recordName: "<value>",
  pdfBinary: "<value>",
};
```

## Fields

| Field                           | Type                            | Required                        | Description                     |
| ------------------------------- | ------------------------------- | ------------------------------- | ------------------------------- |
| `recordName`                    | *string*                        | :heavy_check_mark:              | Name/identifier of the document |
| `pdfBinary`                     | *string*                        | :heavy_check_mark:              | Base64 encoded PDF binary data  |
| `orgId`                         | *string*                        | :heavy_minus_sign:              | Organization ID (optional)      |