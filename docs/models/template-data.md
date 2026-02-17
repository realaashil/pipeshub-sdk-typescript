# TemplateData

Dynamic data to populate the email template. Required fields depend on <code>emailTemplateType</code>.<br><br>
<b>Template Data Requirements:</b><br>
<ul>
<li><b>loginWithOTP:</b> See <code>LoginWithOTPTemplateData</code> - requires <code>name</code>, <code>otp</code></li>
<li><b>resetPassword:</b> See <code>ResetPasswordTemplateData</code> - requires <code>name</code>, <code>link</code></li>
<li><b>accountCreation:</b> See <code>AccountCreationTemplateData</code> - requires <code>orgName</code>, <code>link</code></li>
<li><b>appuserInvite:</b> See <code>AppUserInviteTemplateData</code> - requires <code>invitee</code>, <code>orgName</code>, <code>link</code></li>
<li><b>suspiciousLoginAttempt:</b> See <code>SuspiciousLoginTemplateData</code> - requires <code>link</code></li>
</ul>



## Supported Types

### `models.LoginWithOTPTemplateData`

```typescript
const value: models.LoginWithOTPTemplateData = {
  name: "John Doe",
  otp: "123456",
};
```

### `models.ResetPasswordTemplateData`

```typescript
const value: models.ResetPasswordTemplateData = {
  name: "John Doe",
  link: "https://app.pipeshub.com/reset-password?token=abc123xyz",
};
```

### `models.AccountCreationTemplateData`

```typescript
const value: models.AccountCreationTemplateData = {
  orgName: "Acme Corporation",
  link: "https://app.pipeshub.com/login",
};
```

### `models.AppUserInviteTemplateData`

```typescript
const value: models.AppUserInviteTemplateData = {
  invitee: "Admin User",
  orgName: "Acme Corporation",
  link: "https://app.pipeshub.com/invite?token=invite123abc",
};
```

### `models.SuspiciousLoginTemplateData`

```typescript
const value: models.SuspiciousLoginTemplateData = {
  link: "https://app.pipeshub.com/support",
};
```

