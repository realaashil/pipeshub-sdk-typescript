# UserType

Type of credentials: 'individual' for OAuth, 'business' for service account

## Example Usage

```typescript
import { UserType } from "pipeshub/models";

let value: UserType = "business";
```

## Values

This is an open enum. Unrecognized values will be captured as the `Unrecognized<string>` branded type.

```typescript
"individual" | "business" | Unrecognized<string>
```