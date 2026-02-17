# GetUserCreatedTeamsData

## Example Usage

```typescript
import { GetUserCreatedTeamsData } from "pipeshub/models/operations";

let value: GetUserCreatedTeamsData = {};
```

## Fields

| Field                                                                                         | Type                                                                                          | Required                                                                                      | Description                                                                                   |
| --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| `team`                                                                                        | [models.Team](../../models/team.md)                                                           | :heavy_minus_sign:                                                                            | N/A                                                                                           |
| `currentRole`                                                                                 | [operations.CurrentRole](../../models/operations/current-role.md)                             | :heavy_minus_sign:                                                                            | User's current role (none if no longer a member)                                              |
| `createdAt`                                                                                   | [Date](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) | :heavy_minus_sign:                                                                            | N/A                                                                                           |