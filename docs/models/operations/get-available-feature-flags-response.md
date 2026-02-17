# GetAvailableFeatureFlagsResponse

Feature flags retrieved

## Example Usage

```typescript
import { GetAvailableFeatureFlagsResponse } from "pipeshub/models/operations";

let value: GetAvailableFeatureFlagsResponse = {
  featureFlags: [
    {
      key: "ENABLE_BETA_CONNECTORS",
      label: "Enable Beta Connectors",
    },
  ],
};
```

## Fields

| Field                                                | Type                                                 | Required                                             | Description                                          |
| ---------------------------------------------------- | ---------------------------------------------------- | ---------------------------------------------------- | ---------------------------------------------------- |
| `featureFlags`                                       | [models.FeatureFlag](../../models/feature-flag.md)[] | :heavy_minus_sign:                                   | N/A                                                  |