# ScheduleConfig

Schedule configuration for crawling jobs. The structure varies based on <code>scheduleType</code>.<br><br>
<b>Schedule Type Configurations:</b><br>
<ul>
<li><b>hourly:</b> <code>minute</code>, <code>interval</code> (optional)</li>
<li><b>daily:</b> <code>hour</code>, <code>minute</code></li>
<li><b>weekly:</b> <code>daysOfWeek</code>, <code>hour</code>, <code>minute</code></li>
<li><b>monthly:</b> <code>dayOfMonth</code>, <code>hour</code>, <code>minute</code></li>
<li><b>custom:</b> <code>cronExpression</code>, <code>description</code> (optional)</li>
<li><b>once:</b> <code>scheduledTime</code></li>
</ul>



## Supported Types

### `models.HourlyScheduleConfig`

```typescript
const value: models.HourlyScheduleConfig = {
  scheduleType: "hourly",
  minute: 30,
};
```

### `models.DailyScheduleConfig`

```typescript
const value: models.DailyScheduleConfig = {
  scheduleType: "daily",
  hour: 2,
  minute: 0,
};
```

### `models.WeeklyScheduleConfig`

```typescript
const value: models.WeeklyScheduleConfig = {
  scheduleType: "weekly",
  daysOfWeek: [
    1,
    3,
    5,
  ],
  hour: 3,
  minute: 0,
};
```

### `models.MonthlyScheduleConfig`

```typescript
const value: models.MonthlyScheduleConfig = {
  scheduleType: "monthly",
  dayOfMonth: 1,
  hour: 4,
  minute: 0,
};
```

### `models.CustomScheduleConfig`

```typescript
const value: models.CustomScheduleConfig = {
  scheduleType: "custom",
  cronExpression: "0 2 * * *",
  description: "Run daily at 2:00 AM",
};
```

### `models.OnceScheduleConfig`

```typescript
const value: models.OnceScheduleConfig = {
  scheduleType: "once",
  scheduledTime: new Date("2024-12-25T10:00:00Z"),
};
```

