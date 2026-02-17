# Permissions

Default permission level for shared access

## Example Usage

```typescript
import { Permissions } from "pipeshub/models";

let value: Permissions = "owner";
```

## Values

This is an open enum. Unrecognized values will be captured as the `Unrecognized<string>` branded type.

```typescript
"owner" | "editor" | "commentator" | "readonly" | Unrecognized<string>
```