# Attachment

## Example Usage

```typescript
import { Attachment } from "pipeshub/models";

let value: Attachment = {
  filename: "report.pdf",
  contentType: "application/pdf",
};
```

## Fields

| Field                                             | Type                                              | Required                                          | Description                                       | Example                                           |
| ------------------------------------------------- | ------------------------------------------------- | ------------------------------------------------- | ------------------------------------------------- | ------------------------------------------------- |
| `filename`                                        | *string*                                          | :heavy_minus_sign:                                | Name of the attachment file                       | report.pdf                                        |
| `content`                                         | *string*                                          | :heavy_minus_sign:                                | Base64-encoded file content or raw string content |                                                   |
| `contentType`                                     | *string*                                          | :heavy_minus_sign:                                | MIME type of the attachment                       | application/pdf                                   |