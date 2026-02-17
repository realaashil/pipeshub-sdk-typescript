# SuspiciousLoginTemplateData

Template data for suspicious login attempt security alert email

## Example Usage

```typescript
import { SuspiciousLoginTemplateData } from "pipeshub/models";

let value: SuspiciousLoginTemplateData = {
  link: "https://app.pipeshub.com/support",
};
```

## Fields

| Field                                                 | Type                                                  | Required                                              | Description                                           | Example                                               |
| ----------------------------------------------------- | ----------------------------------------------------- | ----------------------------------------------------- | ----------------------------------------------------- | ----------------------------------------------------- |
| `link`                                                | *string*                                              | :heavy_check_mark:                                    | Support contact URL for reporting unauthorized access | https://app.pipeshub.com/support                      |