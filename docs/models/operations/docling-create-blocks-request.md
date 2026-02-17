# DoclingCreateBlocksRequest

Request payload

## Example Usage

```typescript
import { DoclingCreateBlocksRequest } from "pipeshub/models/operations";

let value: DoclingCreateBlocksRequest = {
  parseResult: "<value>",
};
```

## Fields

| Field                                        | Type                                         | Required                                     | Description                                  |
| -------------------------------------------- | -------------------------------------------- | -------------------------------------------- | -------------------------------------------- |
| `parseResult`                                | *string*                                     | :heavy_check_mark:                           | JSON-encoded DoclingDocument from /parse-pdf |
| `pageNumber`                                 | *number*                                     | :heavy_minus_sign:                           | Optional - process specific page only        |