# GetOnboardingStatusData

## Example Usage

```typescript
import { GetOnboardingStatusData } from "pipeshub/models/operations";

let value: GetOnboardingStatusData = {
  isCompleted: false,
  currentStep: "invite_team",
  completedSteps: [
    "org_profile",
    "admin_setup",
  ],
  completionPercentage: 40,
};
```

## Fields

| Field                                                | Type                                                 | Required                                             | Description                                          | Example                                              |
| ---------------------------------------------------- | ---------------------------------------------------- | ---------------------------------------------------- | ---------------------------------------------------- | ---------------------------------------------------- |
| `isCompleted`                                        | *boolean*                                            | :heavy_minus_sign:                                   | Whether onboarding is fully complete                 | false                                                |
| `currentStep`                                        | *string*                                             | :heavy_minus_sign:                                   | Current active onboarding step                       | invite_team                                          |
| `completedSteps`                                     | *string*[]                                           | :heavy_minus_sign:                                   | N/A                                                  | [<br/>"org_profile",<br/>"admin_setup"<br/>]         |
| `completionPercentage`                               | *number*                                             | :heavy_minus_sign:                                   | N/A                                                  | 40                                                   |
| `steps`                                              | [operations.Step](../../models/operations/step.md)[] | :heavy_minus_sign:                                   | N/A                                                  |                                                      |