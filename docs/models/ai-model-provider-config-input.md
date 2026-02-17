# AIModelProviderConfigInput

## Example Usage

```typescript
import { AIModelProviderConfigInput } from "pipeshub/models";

let value: AIModelProviderConfigInput = {
  provider: "<value>",
  configuration: {},
};
```

## Fields

| Field                                                                                            | Type                                                                                             | Required                                                                                         | Description                                                                                      |
| ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ |
| `provider`                                                                                       | *string*                                                                                         | :heavy_check_mark:                                                                               | AI provider name                                                                                 |
| `configuration`                                                                                  | [models.AIModelProviderConfigConfiguration](../models/ai-model-provider-config-configuration.md) | :heavy_check_mark:                                                                               | N/A                                                                                              |
| `isMultimodal`                                                                                   | *boolean*                                                                                        | :heavy_minus_sign:                                                                               | Whether the model supports multimodal input                                                      |
| `isReasoning`                                                                                    | *boolean*                                                                                        | :heavy_minus_sign:                                                                               | Whether the model supports reasoning                                                             |
| `isDefault`                                                                                      | *boolean*                                                                                        | :heavy_minus_sign:                                                                               | Whether this should be the default model                                                         |
| `contextLength`                                                                                  | *number*                                                                                         | :heavy_minus_sign:                                                                               | Context length for the model                                                                     |