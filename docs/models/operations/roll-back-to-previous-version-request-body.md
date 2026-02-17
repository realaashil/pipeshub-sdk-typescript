# RollBackToPreviousVersionRequestBody

Request payload

## Example Usage

```typescript
import { RollBackToPreviousVersionRequestBody } from "pipeshub/models/operations";

let value: RollBackToPreviousVersionRequestBody = {
  version: "2",
  note: "Reverting to version 2 due to incorrect data in version 3",
};
```

## Fields

| Field                                                     | Type                                                      | Required                                                  | Description                                               | Example                                                   |
| --------------------------------------------------------- | --------------------------------------------------------- | --------------------------------------------------------- | --------------------------------------------------------- | --------------------------------------------------------- |
| `version`                                                 | *string*                                                  | :heavy_check_mark:                                        | Version number to rollback to (0-indexed)                 | 2                                                         |
| `note`                                                    | *string*                                                  | :heavy_check_mark:                                        | Reason for rollback (required for audit trail)            | Reverting to version 2 due to incorrect data in version 3 |