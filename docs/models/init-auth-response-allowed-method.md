# InitAuthResponseAllowedMethod

## Example Usage

```typescript
import { InitAuthResponseAllowedMethod } from "pipeshub/models";

let value: InitAuthResponseAllowedMethod = "microsoft";
```

## Values

This is an open enum. Unrecognized values will be captured as the `Unrecognized<string>` branded type.

```typescript
"samlSso" | "otp" | "password" | "google" | "microsoft" | "azureAd" | "oauth" | Unrecognized<string>
```