# SendEmailData

## Example Usage

```typescript
import { SendEmailData } from "pipeshub/models/operations";

let value: SendEmailData = {
  status: true,
  data: "Email sent",
};
```

## Fields

| Field                                   | Type                                    | Required                                | Description                             | Example                                 |
| --------------------------------------- | --------------------------------------- | --------------------------------------- | --------------------------------------- | --------------------------------------- |
| `status`                                | *boolean*                               | :heavy_minus_sign:                      | Whether the email was sent successfully | true                                    |
| `data`                                  | *string*                                | :heavy_minus_sign:                      | Success message                         | Email sent                              |