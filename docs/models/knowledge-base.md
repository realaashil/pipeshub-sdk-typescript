# KnowledgeBase

## Example Usage

```typescript
import { KnowledgeBase } from "pipeshub/models";

let value: KnowledgeBase = {
  name: "<value>",
  orgId: "<id>",
};
```

## Fields

| Field                                              | Type                                               | Required                                           | Description                                        |
| -------------------------------------------------- | -------------------------------------------------- | -------------------------------------------------- | -------------------------------------------------- |
| `key`                                              | *string*                                           | :heavy_minus_sign:                                 | Unique knowledge base identifier                   |
| `name`                                             | *string*                                           | :heavy_check_mark:                                 | Name of the knowledge base                         |
| `orgId`                                            | *string*                                           | :heavy_check_mark:                                 | Organization ID                                    |
| `createdAtTimestamp`                               | *number*                                           | :heavy_minus_sign:                                 | Creation timestamp                                 |
| `updatedAtTimestamp`                               | *number*                                           | :heavy_minus_sign:                                 | Last update timestamp                              |
| `userRole`                                         | [models.UserRoleEnum](../models/user-role-enum.md) | :heavy_minus_sign:                                 | User's role in this knowledge base                 |
| `isDeleted`                                        | *boolean*                                          | :heavy_minus_sign:                                 | Whether the knowledge base is deleted              |