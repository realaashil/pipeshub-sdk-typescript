# ConnectorServices

## Overview

### Available Operations

* [reindexFailedRecords](#reindexfailedrecords) - [Connector Service] Reindex all failed records

## reindexFailedRecords

⚠️ <b>INTERNAL SERVICE ENDPOINT</b><br><br>

Trigger reindexing of all failed records for a specific connector.<br><br>

<b>Service:</b> Connector Service<br>
<b>Port:</b> 8088<br>
<b>Base URL:</b> <code>http://localhost:8088</code><br><br>

<b>Authentication:</b> Requires scoped service token


### Example Usage

<!-- UsageSnippet language="typescript" operationID="connectorReindexFailedRecords" method="post" path="/connector/api/v1/records/reindex-failed" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
});

async function run() {
  const result = await pipeshub.connectorServices.reindexFailedRecords({
    scopedToken: process.env["PIPESHUB_SCOPED_TOKEN"] ?? "",
  }, {});

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { connectorServicesReindexFailedRecords } from "pipeshub/funcs/connector-services-reindex-failed-records.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
});

async function run() {
  const res = await connectorServicesReindexFailedRecords(pipeshub, {
    scopedToken: process.env["PIPESHUB_SCOPED_TOKEN"] ?? "",
  }, {});
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("connectorServicesReindexFailedRecords failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.ConnectorReindexFailedRecordsRequest](../../models/operations/connector-reindex-failed-records-request.md)                                                         | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `security`                                                                                                                                                                     | [operations.ConnectorReindexFailedRecordsSecurity](../../models/operations/connector-reindex-failed-records-security.md)                                                       | :heavy_check_mark:                                                                                                                                                             | The security requirements to use for the request.                                                                                                                              |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |
| `options.serverURL`                                                                                                                                                            | *string*                                                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                             | An optional server URL to use.                                                                                                                                                 |

### Response

**Promise\<[operations.ConnectorReindexFailedRecordsResponse](../../models/operations/connector-reindex-failed-records-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |