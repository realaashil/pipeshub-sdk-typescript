# QueryServiceHealthCheckRequest

## Example Usage

```typescript
import { QueryServiceHealthCheckRequest } from "pipeshub/models/operations";

let value: QueryServiceHealthCheckRequest = {
  modelType: "llm",
  body: {
    provider: "<value>",
    configuration: {},
  },
};
```

## Fields

| Field                                                                                                               | Type                                                                                                                | Required                                                                                                            | Description                                                                                                         |
| ------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| `modelType`                                                                                                         | [operations.ModelType](../../models/operations/model-type.md)                                                       | :heavy_check_mark:                                                                                                  | Type of model to health check                                                                                       |
| `body`                                                                                                              | [operations.QueryServiceHealthCheckRequestBody](../../models/operations/query-service-health-check-request-body.md) | :heavy_check_mark:                                                                                                  | Request payload                                                                                                     |