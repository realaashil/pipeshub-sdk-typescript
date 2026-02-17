# KBPermission

## Example Usage

```typescript
import { KBPermission } from "pipeshub/models";

let value: KBPermission = {};
```

## Fields

| Field                                                      | Type                                                       | Required                                                   | Description                                                |
| ---------------------------------------------------------- | ---------------------------------------------------------- | ---------------------------------------------------------- | ---------------------------------------------------------- |
| `userId`                                                   | *string*                                                   | :heavy_minus_sign:                                         | User ID                                                    |
| `teamId`                                                   | *string*                                                   | :heavy_minus_sign:                                         | Team ID                                                    |
| `role`                                                     | [models.KBPermissionRole](../models/kb-permission-role.md) | :heavy_minus_sign:                                         | Permission role                                            |
| `kbId`                                                     | *string*                                                   | :heavy_minus_sign:                                         | Knowledge base ID                                          |
| `grantedBy`                                                | *string*                                                   | :heavy_minus_sign:                                         | User ID who granted the permission                         |
| `grantedAt`                                                | *number*                                                   | :heavy_minus_sign:                                         | Timestamp when permission was granted                      |