# QueryServiceHealthCheckRequestBody

Request payload

## Example Usage

```typescript
import { QueryServiceHealthCheckRequestBody } from "pipeshub/models/operations";

let value: QueryServiceHealthCheckRequestBody = {
  provider: "<value>",
  configuration: {},
};
```

## Fields

| Field                                                                | Type                                                                 | Required                                                             | Description                                                          |
| -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- |
| `provider`                                                           | *string*                                                             | :heavy_check_mark:                                                   | Model provider (openai, anthropic, ollama, etc.)                     |
| `configuration`                                                      | [operations.Configuration](../../models/operations/configuration.md) | :heavy_check_mark:                                                   | N/A                                                                  |
| `isMultimodal`                                                       | *boolean*                                                            | :heavy_minus_sign:                                                   | Whether model supports vision/images                                 |