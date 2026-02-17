# QueryServiceSearchRequest

Request payload

## Example Usage

```typescript
import { QueryServiceSearchRequest } from "pipeshub/models/operations";

let value: QueryServiceSearchRequest = {
  query: "How do I configure SSO?",
};
```

## Fields

| Field                                                                                           | Type                                                                                            | Required                                                                                        | Description                                                                                     | Example                                                                                         |
| ----------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| `query`                                                                                         | *string*                                                                                        | :heavy_check_mark:                                                                              | Search query text                                                                               | How do I configure SSO?                                                                         |
| `limit`                                                                                         | *number*                                                                                        | :heavy_minus_sign:                                                                              | Maximum number of results                                                                       |                                                                                                 |
| `filters`                                                                                       | [operations.QueryServiceSearchFilters](../../models/operations/query-service-search-filters.md) | :heavy_minus_sign:                                                                              | Optional filters (e.g., kb IDs)                                                                 |                                                                                                 |