# AppUserInviteTemplateData

Template data for user invitation email

## Example Usage

```typescript
import { AppUserInviteTemplateData } from "pipeshub/models";

let value: AppUserInviteTemplateData = {
  invitee: "Admin User",
  orgName: "Acme Corporation",
  link: "https://app.pipeshub.com/invite?token=invite123abc",
};
```

## Fields

| Field                                                 | Type                                                  | Required                                              | Description                                           | Example                                               |
| ----------------------------------------------------- | ----------------------------------------------------- | ----------------------------------------------------- | ----------------------------------------------------- | ----------------------------------------------------- |
| `invitee`                                             | *string*                                              | :heavy_check_mark:                                    | Name of the person who sent the invitation            | Admin User                                            |
| `orgName`                                             | *string*                                              | :heavy_check_mark:                                    | Name of the organization the user is being invited to | Acme Corporation                                      |
| `link`                                                | *string*                                              | :heavy_check_mark:                                    | Invitation acceptance URL with secure token           | https://app.pipeshub.com/invite?token=invite123abc    |