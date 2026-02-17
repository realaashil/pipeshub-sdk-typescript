# QueueStats

Aggregate statistics for the crawling job queue

## Example Usage

```typescript
import { QueueStats } from "pipeshub/models";

let value: QueueStats = {
  waiting: 5,
  active: 2,
  completed: 150,
  failed: 3,
  delayed: 10,
  paused: 1,
  repeatable: 8,
  total: 171,
};
```

## Fields

| Field                                                         | Type                                                          | Required                                                      | Description                                                   | Example                                                       |
| ------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- |
| `waiting`                                                     | *number*                                                      | :heavy_check_mark:                                            | Number of jobs waiting to be processed                        | 5                                                             |
| `active`                                                      | *number*                                                      | :heavy_check_mark:                                            | Number of jobs currently being processed                      | 2                                                             |
| `completed`                                                   | *number*                                                      | :heavy_check_mark:                                            | Number of successfully completed jobs (limited to recent)     | 150                                                           |
| `failed`                                                      | *number*                                                      | :heavy_check_mark:                                            | Number of failed jobs (limited to recent)                     | 3                                                             |
| `delayed`                                                     | *number*                                                      | :heavy_check_mark:                                            | Number of jobs scheduled for future execution                 | 10                                                            |
| `paused`                                                      | *number*                                                      | :heavy_check_mark:                                            | Number of manually paused jobs                                | 1                                                             |
| `repeatable`                                                  | *number*                                                      | :heavy_check_mark:                                            | Number of repeatable job configurations (recurring schedules) | 8                                                             |
| `total`                                                       | *number*                                                      | :heavy_check_mark:                                            | Total count of all jobs across all states                     | 171                                                           |