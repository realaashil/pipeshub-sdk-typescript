# UpdateUserDesignationRequest

## Example Usage

```typescript
import { UpdateUserDesignationRequest } from "pipeshub/models/operations";

let value: UpdateUserDesignationRequest = {
  id: "507f1f77bcf86cd799439011",
  body: {
    designation: "Senior Software Engineer",
  },
};
```

## Fields

| Field                                                                                                          | Type                                                                                                           | Required                                                                                                       | Description                                                                                                    | Example                                                                                                        |
| -------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| `id`                                                                                                           | *string*                                                                                                       | :heavy_check_mark:                                                                                             | User ID (24-character MongoDB ObjectId)                                                                        | 507f1f77bcf86cd799439011                                                                                       |
| `body`                                                                                                         | [operations.UpdateUserDesignationRequestBody](../../models/operations/update-user-designation-request-body.md) | :heavy_check_mark:                                                                                             | Request payload                                                                                                |                                                                                                                |