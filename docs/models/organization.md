# Organization

## Example Usage

```typescript
import { Organization } from "pipeshub/models";

let value: Organization = {
  domain: "ugly-coliseum.name",
  contactEmail: "Florida80@yahoo.com",
  accountType: "individual",
};
```

## Fields

| Field                                                                    | Type                                                                     | Required                                                                 | Description                                                              |
| ------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ |
| `id`                                                                     | *string*                                                                 | :heavy_minus_sign:                                                       | Unique organization identifier                                           |
| `slug`                                                                   | *string*                                                                 | :heavy_minus_sign:                                                       | Unique slug for the organization                                         |
| `registeredName`                                                         | *string*                                                                 | :heavy_minus_sign:                                                       | Registered name                                                          |
| `shortName`                                                              | *string*                                                                 | :heavy_minus_sign:                                                       | Short name or display name                                               |
| `domain`                                                                 | *string*                                                                 | :heavy_check_mark:                                                       | Organization domain                                                      |
| `contactEmail`                                                           | *string*                                                                 | :heavy_check_mark:                                                       | Contact email address                                                    |
| `accountType`                                                            | [models.OrganizationAccountType](../models/organization-account-type.md) | :heavy_check_mark:                                                       | Type of account                                                          |
| `onBoardingStatus`                                                       | [models.OnBoardingStatus](../models/on-boarding-status.md)               | :heavy_minus_sign:                                                       | Onboarding status                                                        |
| `isDeleted`                                                              | *boolean*                                                                | :heavy_minus_sign:                                                       | Soft delete flag                                                         |
| `createdAt`                                                              | *number*                                                                 | :heavy_minus_sign:                                                       | Creation timestamp                                                       |
| `updatedAt`                                                              | *number*                                                                 | :heavy_minus_sign:                                                       | Last update timestamp                                                    |