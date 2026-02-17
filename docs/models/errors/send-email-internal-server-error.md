# SendEmailInternalServerError

Internal server error. Email sending failed due to:<br>
<ul>
<li>SMTP server connection failure</li>
<li>Authentication failure with SMTP server</li>
<li>Template compilation error</li>
<li>Network issues</li>
</ul>


## Example Usage

```typescript
import { SendEmailInternalServerError } from "pipeshub/models/errors";

// No examples available for this model
```

## Fields

| Field                | Type                 | Required             | Description          | Example              |
| -------------------- | -------------------- | -------------------- | -------------------- | -------------------- |
| `error`              | *string*             | :heavy_minus_sign:   | N/A                  | Failed to send email |