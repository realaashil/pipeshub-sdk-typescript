# SendEmailResponse

Email sent successfully and logged to database

## Example Usage

```typescript
import { SendEmailResponse } from "pipeshub/models/operations";

let value: SendEmailResponse = {
  data: {
    status: true,
    data: "Email sent",
  },
};
```

## Fields

| Field                                                                  | Type                                                                   | Required                                                               | Description                                                            |
| ---------------------------------------------------------------------- | ---------------------------------------------------------------------- | ---------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| `data`                                                                 | [operations.SendEmailData](../../models/operations/send-email-data.md) | :heavy_minus_sign:                                                     | N/A                                                                    |