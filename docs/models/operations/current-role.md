# CurrentRole

User's current role (none if no longer a member)

## Example Usage

```typescript
import { CurrentRole } from "pipeshub/models/operations";

let value: CurrentRole = "member";
```

## Values

This is an open enum. Unrecognized values will be captured as the `Unrecognized<string>` branded type.

```typescript
"owner" | "admin" | "member" | "viewer" | "none" | Unrecognized<string>
```