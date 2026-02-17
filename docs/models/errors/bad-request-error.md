# BadRequestError

Bad request. Possible reasons:<br>
<ul>
<li>SMTP not configured properly (missing host, port, or fromEmail)</li>
<li>Invalid or unknown email template type</li>
<li>Missing required templateData fields for the selected template</li>
<li>Invalid email format in sendEmailTo or sendCcTo</li>
</ul>


## Example Usage

```typescript
import { BadRequestError } from "pipeshub/models/errors";

// No examples available for this model
```

## Fields

| Field                        | Type                         | Required                     | Description                  | Example                      |
| ---------------------------- | ---------------------------- | ---------------------------- | ---------------------------- | ---------------------------- |
| `error`                      | *string*                     | :heavy_minus_sign:           | N/A                          | Smtp not configured properly |