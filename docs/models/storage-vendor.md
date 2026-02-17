# StorageVendor

Storage backend where the file is stored

## Example Usage

```typescript
import { StorageVendor } from "pipeshub/models";

let value: StorageVendor = "s3";
```

## Values

This is an open enum. Unrecognized values will be captured as the `Unrecognized<string>` branded type.

```typescript
"s3" | "azureBlob" | "local" | Unrecognized<string>
```