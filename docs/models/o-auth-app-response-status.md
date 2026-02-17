# OAuthAppResponseStatus

App status

## Example Usage

```typescript
import { OAuthAppResponseStatus } from "pipeshub/models";

let value: OAuthAppResponseStatus = "revoked";
```

## Values

This is an open enum. Unrecognized values will be captured as the `Unrecognized<string>` branded type.

```typescript
"active" | "suspended" | "revoked" | Unrecognized<string>
```