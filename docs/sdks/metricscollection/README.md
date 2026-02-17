# MetricsCollection

## Overview

### Available Operations

* [getConfiguration](#getconfiguration) - Get metrics collection configuration
* [setPushInterval](#setpushinterval) - Configure metrics push interval
* [setServerUrl](#setserverurl) - Configure metrics server URL

## getConfiguration

Retrieve the current metrics collection configuration including:
- Whether collection is enabled
- Push interval settings
- Server URL configuration
- Instance identification

**Admin Access Required:** This endpoint requires administrator privileges.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="getMetricsCollection" method="get" path="/configurationManager/metricsCollection" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.metricsCollection.getConfiguration();

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { metricsCollectionGetConfiguration } from "pipeshub/funcs/metrics-collection-get-configuration.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await metricsCollectionGetConfiguration(pipeshub);
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("metricsCollectionGetConfiguration failed:", res.error);
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

**Promise\<[models.MetricsCollectionConfig](../../models/metrics-collection-config.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## setPushInterval

Set how frequently collected metrics are pushed to the remote server.

**Interval Guidelines:**
- Minimum: 1000ms (1 second) - for real-time monitoring
- Recommended: 60000ms (1 minute) - balanced performance
- Maximum: No hard limit, but longer intervals may delay insights

**Performance Considerations:**
- Shorter intervals provide more real-time data but increase network traffic
- Longer intervals reduce overhead but delay metric visibility
- Changes take effect on the next push cycle

**Admin Access Required:** This endpoint requires administrator privileges.


### Example Usage: default

<!-- UsageSnippet language="typescript" operationID="setMetricsPushInterval" method="patch" path="/configurationManager/metricsCollection/pushInterval" example="default" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.metricsCollection.setPushInterval({
    pushIntervalMs: 60000,
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { metricsCollectionSetPushInterval } from "pipeshub/funcs/metrics-collection-set-push-interval.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await metricsCollectionSetPushInterval(pipeshub, {
    pushIntervalMs: 60000,
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("metricsCollectionSetPushInterval failed:", res.error);
  }
}

run();
```
### Example Usage: lowFrequency

<!-- UsageSnippet language="typescript" operationID="setMetricsPushInterval" method="patch" path="/configurationManager/metricsCollection/pushInterval" example="lowFrequency" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.metricsCollection.setPushInterval({
    pushIntervalMs: 300000,
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { metricsCollectionSetPushInterval } from "pipeshub/funcs/metrics-collection-set-push-interval.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await metricsCollectionSetPushInterval(pipeshub, {
    pushIntervalMs: 300000,
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("metricsCollectionSetPushInterval failed:", res.error);
  }
}

run();
```
### Example Usage: realtime

<!-- UsageSnippet language="typescript" operationID="setMetricsPushInterval" method="patch" path="/configurationManager/metricsCollection/pushInterval" example="realtime" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.metricsCollection.setPushInterval({
    pushIntervalMs: 10000,
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { metricsCollectionSetPushInterval } from "pipeshub/funcs/metrics-collection-set-push-interval.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await metricsCollectionSetPushInterval(pipeshub, {
    pushIntervalMs: 10000,
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("metricsCollectionSetPushInterval failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.SetMetricsPushIntervalRequest](../../models/operations/set-metrics-push-interval-request.md)                                                                       | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.SetMetricsPushIntervalResponse](../../models/operations/set-metrics-push-interval-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## setServerUrl

Set the remote server URL where metrics will be pushed.

**Use Cases:**
- Self-hosted analytics: Point to your own Prometheus-compatible endpoint
- Custom monitoring: Integrate with your organization's monitoring stack
- Development: Use a local endpoint for testing

**URL Requirements:**
- Must be a valid URL (http or https)
- Server must accept POST requests with JSON payload
- Server should return 2xx status for successful pushes

**Admin Access Required:** This endpoint requires administrator privileges.


### Example Usage: localDev

<!-- UsageSnippet language="typescript" operationID="setMetricsServerUrl" method="patch" path="/configurationManager/metricsCollection/serverUrl" example="localDev" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.metricsCollection.setServerUrl({
    serverUrl: "http://localhost:9090/metrics",
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { metricsCollectionSetServerUrl } from "pipeshub/funcs/metrics-collection-set-server-url.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await metricsCollectionSetServerUrl(pipeshub, {
    serverUrl: "http://localhost:9090/metrics",
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("metricsCollectionSetServerUrl failed:", res.error);
  }
}

run();
```
### Example Usage: selfHosted

<!-- UsageSnippet language="typescript" operationID="setMetricsServerUrl" method="patch" path="/configurationManager/metricsCollection/serverUrl" example="selfHosted" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.metricsCollection.setServerUrl({
    serverUrl: "https://metrics.mycompany.com/collect",
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { metricsCollectionSetServerUrl } from "pipeshub/funcs/metrics-collection-set-server-url.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await metricsCollectionSetServerUrl(pipeshub, {
    serverUrl: "https://metrics.mycompany.com/collect",
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("metricsCollectionSetServerUrl failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.SetMetricsServerUrlRequest](../../models/operations/set-metrics-server-url-request.md)                                                                             | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.SetMetricsServerUrlResponse](../../models/operations/set-metrics-server-url-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |