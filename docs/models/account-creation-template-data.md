# AccountCreationTemplateData

Template data for organization account creation welcome email

## Example Usage

```typescript
import { AccountCreationTemplateData } from "pipeshub/models";

let value: AccountCreationTemplateData = {
  orgName: "Acme Corporation",
  link: "https://app.pipeshub.com/login",
};
```

## Fields

| Field                                  | Type                                   | Required                               | Description                            | Example                                |
| -------------------------------------- | -------------------------------------- | -------------------------------------- | -------------------------------------- | -------------------------------------- |
| `orgName`                              | *string*                               | :heavy_check_mark:                     | Name of the newly created organization | Acme Corporation                       |
| `link`                                 | *string*                               | :heavy_check_mark:                     | Login URL for the platform             | https://app.pipeshub.com/login         |