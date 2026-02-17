# EmailTemplateType

Type of email template to use. Each template has specific `templateData` requirements:
- `loginWithOTP`: OTP authentication email
- `resetPassword`: Password reset link email
- `accountCreation`: Welcome email for new organizations
- `appuserInvite`: Invitation email to join an organization
- `suspiciousLoginAttempt`: Security alert for multiple failed OTP attempts


## Example Usage

```typescript
import { EmailTemplateType } from "pipeshub/models";

let value: EmailTemplateType = "loginWithOTP";
```

## Values

```typescript
"loginWithOTP" | "resetPassword" | "accountCreation" | "appuserInvite" | "suspiciousLoginAttempt"
```