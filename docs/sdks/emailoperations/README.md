# EmailOperations

## Overview

### Available Operations

* [send](#send) - Send a transactional email

## send

Send a transactional email using the configured SMTP server with a pre-defined template.<br><br>

<b>Overview:</b><br>
This is an internal service endpoint used by other PipesHub services to send transactional emails.
It uses Handlebars templates to generate HTML emails with dynamic content. All sent emails are
logged to the database for audit purposes.<br><br>

<b>Authentication:</b><br>
Requires a scoped token with <code>mail:send</code> scope. This endpoint is not accessible
with regular user JWT tokens - it is designed for service-to-service communication only.<br><br>

<b>Available Templates:</b><br>
<ul>
<li><b>loginWithOTP</b> - Send OTP code for user authentication. Requires: <code>name</code>, <code>otp</code></li>
<li><b>resetPassword</b> - Password reset link. Requires: <code>name</code>, <code>link</code></li>
<li><b>accountCreation</b> - Welcome email for new organizations. Requires: <code>orgName</code>, <code>link</code></li>
<li><b>appuserInvite</b> - Invitation to join organization. Requires: <code>invitee</code>, <code>orgName</code>, <code>link</code></li>
<li><b>suspiciousLoginAttempt</b> - Security alert. Requires: <code>link</code></li>
</ul>

<b>Email Delivery Flow:</b><br>
<ol>
<li>Validate SMTP configuration exists (middleware check)</li>
<li>Validate scoped token has <code>mail:send</code> scope</li>
<li>Select and compile Handlebars template with provided data</li>
<li>Send email via nodemailer using SMTP configuration</li>
<li>Log email metadata to MongoDB (subject, from, to, cc, templateType)</li>
</ol>

<b>Important Notes:</b><br>
<ul>
<li>The "From" address is always taken from SMTP config, not the request body</li>
<li>Failed email sends return 500 with error details</li>
<li>Template mismatches throw "Unknown Template" error</li>
<li>SMTP must be configured before using this endpoint</li>
</ul>

<b>Related Endpoints:</b><br>
<ul>
<li><code>POST /configurationManager/smtpConfig</code> - Configure SMTP server</li>
<li><code>POST /mail/updateSmtpConfig</code> - Reload SMTP configuration at runtime</li>
</ul>


### Example Usage: accountCreation

<!-- UsageSnippet language="typescript" operationID="sendEmail" method="post" path="/mail/emails/sendEmail" example="accountCreation" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
});

async function run() {
  const result = await pipeshub.emailOperations.send({
    scopedToken: process.env["PIPESHUB_SCOPED_TOKEN"] ?? "",
  }, {
    emailTemplateType: "accountCreation",
    sendEmailTo: [
      "admin@neworg.com",
    ],
    subject: "Welcome to PipesHub!",
    templateData: {
      orgName: "New Organization Inc",
      link: "https://app.pipeshub.com/login",
    },
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { emailOperationsSend } from "pipeshub/funcs/email-operations-send.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
});

async function run() {
  const res = await emailOperationsSend(pipeshub, {
    scopedToken: process.env["PIPESHUB_SCOPED_TOKEN"] ?? "",
  }, {
    emailTemplateType: "accountCreation",
    sendEmailTo: [
      "admin@neworg.com",
    ],
    subject: "Welcome to PipesHub!",
    templateData: {
      orgName: "New Organization Inc",
      link: "https://app.pipeshub.com/login",
    },
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("emailOperationsSend failed:", res.error);
  }
}

run();
```
### Example Usage: loginOTP

<!-- UsageSnippet language="typescript" operationID="sendEmail" method="post" path="/mail/emails/sendEmail" example="loginOTP" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
});

async function run() {
  const result = await pipeshub.emailOperations.send({
    scopedToken: process.env["PIPESHUB_SCOPED_TOKEN"] ?? "",
  }, {
    emailTemplateType: "loginWithOTP",
    isAutoEmail: true,
    sendEmailTo: [
      "user@example.com",
    ],
    subject: "Your OTP Code for PipesHub",
    templateData: {
      name: "John Doe",
      otp: "123456",
    },
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { emailOperationsSend } from "pipeshub/funcs/email-operations-send.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
});

async function run() {
  const res = await emailOperationsSend(pipeshub, {
    scopedToken: process.env["PIPESHUB_SCOPED_TOKEN"] ?? "",
  }, {
    emailTemplateType: "loginWithOTP",
    isAutoEmail: true,
    sendEmailTo: [
      "user@example.com",
    ],
    subject: "Your OTP Code for PipesHub",
    templateData: {
      name: "John Doe",
      otp: "123456",
    },
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("emailOperationsSend failed:", res.error);
  }
}

run();
```
### Example Usage: passwordReset

<!-- UsageSnippet language="typescript" operationID="sendEmail" method="post" path="/mail/emails/sendEmail" example="passwordReset" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
});

async function run() {
  const result = await pipeshub.emailOperations.send({
    scopedToken: process.env["PIPESHUB_SCOPED_TOKEN"] ?? "",
  }, {
    emailTemplateType: "resetPassword",
    sendEmailTo: [
      "user@example.com",
    ],
    subject: "Reset Your PipesHub Password",
    templateData: {
      name: "John Doe",
      link: "https://app.pipeshub.com/reset-password?token=abc123xyz",
    },
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { emailOperationsSend } from "pipeshub/funcs/email-operations-send.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
});

async function run() {
  const res = await emailOperationsSend(pipeshub, {
    scopedToken: process.env["PIPESHUB_SCOPED_TOKEN"] ?? "",
  }, {
    emailTemplateType: "resetPassword",
    sendEmailTo: [
      "user@example.com",
    ],
    subject: "Reset Your PipesHub Password",
    templateData: {
      name: "John Doe",
      link: "https://app.pipeshub.com/reset-password?token=abc123xyz",
    },
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("emailOperationsSend failed:", res.error);
  }
}

run();
```
### Example Usage: securityAlert

<!-- UsageSnippet language="typescript" operationID="sendEmail" method="post" path="/mail/emails/sendEmail" example="securityAlert" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
});

async function run() {
  const result = await pipeshub.emailOperations.send({
    scopedToken: process.env["PIPESHUB_SCOPED_TOKEN"] ?? "",
  }, {
    emailTemplateType: "suspiciousLoginAttempt",
    sendEmailTo: [
      "user@example.com",
    ],
    subject: "Security Alert: Suspicious Login Attempt",
    templateData: {
      link: "https://app.pipeshub.com/support",
    },
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { emailOperationsSend } from "pipeshub/funcs/email-operations-send.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
});

async function run() {
  const res = await emailOperationsSend(pipeshub, {
    scopedToken: process.env["PIPESHUB_SCOPED_TOKEN"] ?? "",
  }, {
    emailTemplateType: "suspiciousLoginAttempt",
    sendEmailTo: [
      "user@example.com",
    ],
    subject: "Security Alert: Suspicious Login Attempt",
    templateData: {
      link: "https://app.pipeshub.com/support",
    },
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("emailOperationsSend failed:", res.error);
  }
}

run();
```
### Example Usage: userInvitation

<!-- UsageSnippet language="typescript" operationID="sendEmail" method="post" path="/mail/emails/sendEmail" example="userInvitation" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
});

async function run() {
  const result = await pipeshub.emailOperations.send({
    scopedToken: process.env["PIPESHUB_SCOPED_TOKEN"] ?? "",
  }, {
    emailTemplateType: "appuserInvite",
    sendEmailTo: [
      "newuser@example.com",
    ],
    subject: "You've been invited to join Acme Corp on PipesHub",
    templateData: {
      invitee: "Admin User",
      orgName: "Acme Corp",
      link: "https://app.pipeshub.com/invite?token=invite123",
    },
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { emailOperationsSend } from "pipeshub/funcs/email-operations-send.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
});

async function run() {
  const res = await emailOperationsSend(pipeshub, {
    scopedToken: process.env["PIPESHUB_SCOPED_TOKEN"] ?? "",
  }, {
    emailTemplateType: "appuserInvite",
    sendEmailTo: [
      "newuser@example.com",
    ],
    subject: "You've been invited to join Acme Corp on PipesHub",
    templateData: {
      invitee: "Admin User",
      orgName: "Acme Corp",
      link: "https://app.pipeshub.com/invite?token=invite123",
    },
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("emailOperationsSend failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [models.MailBody](../../models/mail-body.md)                                                                                                                                   | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `security`                                                                                                                                                                     | [operations.SendEmailSecurity](../../models/operations/send-email-security.md)                                                                                                 | :heavy_check_mark:                                                                                                                                                             | The security requirements to use for the request.                                                                                                                              |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.SendEmailResponse](../../models/operations/send-email-response.md)\>**

### Errors

| Error Type                          | Status Code                         | Content Type                        |
| ----------------------------------- | ----------------------------------- | ----------------------------------- |
| errors.BadRequestError              | 400                                 | application/json                    |
| errors.NotFoundError                | 404                                 | application/json                    |
| errors.SendEmailInternalServerError | 500                                 | application/json                    |
| errors.PipeshubDefaultError         | 4XX, 5XX                            | \*/\*                               |