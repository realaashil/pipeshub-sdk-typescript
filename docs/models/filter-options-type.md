# FilterOptionsType

Filter input type

## Example Usage

```typescript
import { FilterOptionsType } from "pipeshub/models";

let value: FilterOptionsType = "select";
```

## Values

This is an open enum. Unrecognized values will be captured as the `Unrecognized<string>` branded type.

```typescript
"select" | "multiselect" | "text" | "boolean" | Unrecognized<string>
```