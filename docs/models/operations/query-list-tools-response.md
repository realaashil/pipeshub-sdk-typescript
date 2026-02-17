# QueryListToolsResponse

## Example Usage

```typescript
import { QueryListToolsResponse } from "pipeshub/models/operations";

let value: QueryListToolsResponse = {};
```

## Fields

| Field                                                             | Type                                                              | Required                                                          | Description                                                       |
| ----------------------------------------------------------------- | ----------------------------------------------------------------- | ----------------------------------------------------------------- | ----------------------------------------------------------------- |
| `name`                                                            | *string*                                                          | :heavy_minus_sign:                                                | Tool name identifier                                              |
| `description`                                                     | *string*                                                          | :heavy_minus_sign:                                                | Human-readable tool description                                   |
| `parameters`                                                      | [operations.ParametersT](../../models/operations/parameters-t.md) | :heavy_minus_sign:                                                | Tool parameter definitions                                        |
| `tags`                                                            | *string*[]                                                        | :heavy_minus_sign:                                                | Tool categorization tags                                          |