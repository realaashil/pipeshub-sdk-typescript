# OAuthAppWithSecretStatus

App status

## Example Usage

```typescript
import { OAuthAppWithSecretStatus } from "pipeshub/models";

let value: OAuthAppWithSecretStatus = "revoked";
```

## Values

This is an open enum. Unrecognized values will be captured as the `Unrecognized<string>` branded type.

```typescript
"active" | "suspended" | "revoked" | Unrecognized<string>
```