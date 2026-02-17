# GetOnboardingStatusResponse

Onboarding status retrieved successfully

## Example Usage

```typescript
import { GetOnboardingStatusResponse } from "pipeshub/models/operations";

let value: GetOnboardingStatusResponse = {
  success: true,
  data: {
    isCompleted: false,
    currentStep: "invite_team",
    completedSteps: [
      "org_profile",
      "admin_setup",
    ],
    completionPercentage: 40,
  },
};
```

## Fields

| Field                                                                                       | Type                                                                                        | Required                                                                                    | Description                                                                                 | Example                                                                                     |
| ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| `success`                                                                                   | *boolean*                                                                                   | :heavy_minus_sign:                                                                          | N/A                                                                                         | true                                                                                        |
| `data`                                                                                      | [operations.GetOnboardingStatusData](../../models/operations/get-onboarding-status-data.md) | :heavy_minus_sign:                                                                          | N/A                                                                                         |                                                                                             |