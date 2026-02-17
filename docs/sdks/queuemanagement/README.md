# QueueManagement

## Overview

### Available Operations

* [getStats](#getstats) - Get queue statistics

## getStats

Retrieve aggregate statistics about the crawling job queue.<br><br>

<b>Overview:</b><br>
Returns real-time statistics about the BullMQ queue including job counts by state,
paused jobs, and repeatable job configurations. Useful for monitoring system health
and capacity planning.<br><br>

<b>Statistics Included:</b><br>
<ul>
<li><b>waiting:</b> Jobs queued and waiting to be processed</li>
<li><b>active:</b> Jobs currently being processed by workers</li>
<li><b>completed:</b> Successfully completed jobs (limited retention)</li>
<li><b>failed:</b> Failed jobs (limited retention)</li>
<li><b>delayed:</b> Jobs scheduled for future execution</li>
<li><b>paused:</b> Manually paused jobs</li>
<li><b>repeatable:</b> Number of repeatable job configurations</li>
<li><b>total:</b> Sum of all job counts</li>
</ul>

<b>Use Cases:</b><br>
<ul>
<li>Monitor queue health and throughput</li>
<li>Identify processing bottlenecks</li>
<li>Track failed job counts for alerting</li>
<li>Capacity planning based on queue depth</li>
</ul>


### Example Usage

<!-- UsageSnippet language="typescript" operationID="getQueueStats" method="get" path="/crawlingManager/stats" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.queueManagement.getStats();

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { queueManagementGetStats } from "pipeshub/funcs/queue-management-get-stats.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await queueManagementGetStats(pipeshub);
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("queueManagementGetStats failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.GetQueueStatsResponse](../../models/operations/get-queue-stats-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |