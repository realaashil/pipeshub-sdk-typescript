# DeleteDocumentByIdResponse

Document deleted successfully

## Example Usage

```typescript
import { DeleteDocumentByIdResponse } from "pipeshub/models/operations";

let value: DeleteDocumentByIdResponse = {
  success: true,
  message: "Document deleted successfully",
  data: {
    isDeleted: true,
  },
};
```

## Fields

| Field                                                                                      | Type                                                                                       | Required                                                                                   | Description                                                                                | Example                                                                                    |
| ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ |
| `success`                                                                                  | *boolean*                                                                                  | :heavy_minus_sign:                                                                         | N/A                                                                                        | true                                                                                       |
| `message`                                                                                  | *string*                                                                                   | :heavy_minus_sign:                                                                         | N/A                                                                                        | Document deleted successfully                                                              |
| `data`                                                                                     | [operations.DeleteDocumentByIdData](../../models/operations/delete-document-by-id-data.md) | :heavy_minus_sign:                                                                         | N/A                                                                                        |                                                                                            |