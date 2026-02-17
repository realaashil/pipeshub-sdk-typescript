# OAuthScopeInfo

Information about an OAuth scope

## Example Usage

```typescript
import { OAuthScopeInfo } from "pipeshub/models";

let value: OAuthScopeInfo = {
  name: "read:records",
  description: "Read access to records",
  category: "Records",
};
```

## Fields

| Field                            | Type                             | Required                         | Description                      | Example                          |
| -------------------------------- | -------------------------------- | -------------------------------- | -------------------------------- | -------------------------------- |
| `name`                           | *string*                         | :heavy_minus_sign:               | Scope identifier                 | read:records                     |
| `description`                    | *string*                         | :heavy_minus_sign:               | Human-readable scope description | Read access to records           |
| `category`                       | *string*                         | :heavy_minus_sign:               | Scope category for grouping      | Records                          |