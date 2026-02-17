# GetStorageConfigStorageType

Currently configured storage type

## Example Usage

```typescript
import { GetStorageConfigStorageType } from "pipeshub/models/operations";

let value: GetStorageConfigStorageType = "local";
```

## Values

This is an open enum. Unrecognized values will be captured as the `Unrecognized<string>` branded type.

```typescript
"local" | "s3" | "azureBlob" | Unrecognized<string>
```