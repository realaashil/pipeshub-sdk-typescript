# GoogleWorkspaceCredentials

Google Workspace service account or OAuth credentials

## Example Usage

```typescript
import { GoogleWorkspaceCredentials } from "pipeshub/models";

let value: GoogleWorkspaceCredentials = {};
```

## Fields

| Field                                                                                                 | Type                                                                                                  | Required                                                                                              | Description                                                                                           |
| ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| `userType`                                                                                            | [models.UserType](../models/user-type.md)                                                             | :heavy_minus_sign:                                                                                    | Type of credentials: 'individual' for OAuth, 'business' for service account                           |
| `credentials`                                                                                         | [models.GoogleWorkspaceCredentialsCredentials](../models/google-workspace-credentials-credentials.md) | :heavy_minus_sign:                                                                                    | Credential data (structure depends on userType)                                                       |