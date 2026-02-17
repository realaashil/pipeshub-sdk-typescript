# QueryService

## Overview

### Available Operations

* [search](#search) - [Query Service] Semantic search
* [chat](#chat) - [Query Service] Chat with knowledge base
* [chatStream](#chatstream) - [Query Service] Streaming chat with knowledge base
* [healthCheck](#healthcheck) - [Query Service] AI model health check
* [listTools](#listtools) - [Query Service] List available agent tools

## search

⚠️ <b>INTERNAL SERVICE ENDPOINT</b><br><br>

Perform semantic search across indexed documents using vector embeddings.<br><br>

<b>Service:</b> Query Service<br>
<b>Port:</b> 8000<br>
<b>Base URL:</b> <code>http://localhost:8000</code><br><br>

<b>Authentication:</b> Requires user JWT token (proxied from main API) or scoped service token<br><br>

<b>How It Works:</b><br>
<ol>
<li>Query is transformed and expanded using LLM</li>
<li>Embeddings are generated for search queries</li>
<li>Vector similarity search in Qdrant</li>
<li>Results filtered by user permissions</li>
<li>Optional knowledge base filtering</li>
</ol>


### Example Usage

<!-- UsageSnippet language="typescript" operationID="queryServiceSearch" method="post" path="/query/api/v1/search" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.queryService.search({
    query: "How do I configure SSO?",
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { queryServiceSearch } from "pipeshub/funcs/query-service-search.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await queryServiceSearch(pipeshub, {
    query: "How do I configure SSO?",
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("queryServiceSearch failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.QueryServiceSearchRequest](../../models/operations/query-service-search-request.md)                                                                                | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |
| `options.serverURL`                                                                                                                                                            | *string*                                                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                             | An optional server URL to use.                                                                                                                                                 |

### Response

**Promise\<[operations.QueryServiceSearchResponse](../../models/operations/query-service-search-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## chat

⚠️ <b>INTERNAL SERVICE ENDPOINT</b><br><br>

Conversational AI endpoint with RAG (Retrieval-Augmented Generation).<br><br>

<b>Service:</b> Query Service<br>
<b>Port:</b> 8000<br>
<b>Base URL:</b> <code>http://localhost:8000</code><br><br>

<b>Authentication:</b> Requires user JWT token (proxied from main API) or scoped service token<br><br>

<b>Features:</b><br>
<ul>
<li>Multi-turn conversation support</li>
<li>Context from knowledge base</li>
<li>Citation of source documents</li>
<li>Multiple chat modes (quick, analysis, deep_research, creative, precise)</li>
<li>Multi-model support (OpenAI, Anthropic, Ollama, etc.)</li>
</ul>


### Example Usage

<!-- UsageSnippet language="typescript" operationID="queryServiceChat" method="post" path="/query/api/v1/chat" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  await pipeshub.queryService.chat({
    query: "<value>",
  });


}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { queryServiceChat } from "pipeshub/funcs/query-service-chat.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await queryServiceChat(pipeshub, {
    query: "<value>",
  });
  if (res.ok) {
    const { value: result } = res;
    
  } else {
    console.log("queryServiceChat failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.QueryServiceChatRequest](../../models/operations/query-service-chat-request.md)                                                                                    | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |
| `options.serverURL`                                                                                                                                                            | *string*                                                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                             | An optional server URL to use.                                                                                                                                                 |

### Response

**Promise\<void\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## chatStream

⚠️ <b>INTERNAL SERVICE ENDPOINT</b><br><br>

Streaming conversational AI endpoint with real-time token delivery.<br><br>

<b>Service:</b> Query Service<br>
<b>Port:</b> 8000<br>
<b>Base URL:</b> <code>http://localhost:8000</code><br><br>

<b>Authentication:</b> Requires user JWT token (proxied from main API) or scoped service token<br><br>

<b>SSE Events:</b><br>
<ul>
<li><code>status</code>: Processing status updates</li>
<li><code>chunk</code>: Token/text chunks</li>
<li><code>citations</code>: Source citations</li>
<li><code>done</code>: Stream complete</li>
<li><code>error</code>: Error occurred</li>
</ul>


### Example Usage

<!-- UsageSnippet language="typescript" operationID="queryServiceChatStream" method="post" path="/query/api/v1/chat/stream" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.queryService.chatStream();

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { queryServiceChatStream } from "pipeshub/funcs/query-service-chat-stream.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await queryServiceChatStream(pipeshub);
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("queryServiceChatStream failed:", res.error);
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
| `options.serverURL`                                                                                                                                                            | *string*                                                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                             | An optional server URL to use.                                                                                                                                                 |

### Response

**Promise\<[string](../../models/.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## healthCheck

⚠️ <b>INTERNAL SERVICE ENDPOINT</b><br><br>

Validate LLM or embedding model configuration.<br><br>

<b>Service:</b> Query Service<br>
<b>Port:</b> 8000<br>
<b>Base URL:</b> <code>http://localhost:8000</code><br><br>

<b>Authentication:</b> Requires scoped service token<br><br>

<b>Model Types:</b>
<ul>
<li><code>llm</code> - Test LLM configuration (text generation)</li>
<li><code>embedding</code> - Test embedding model configuration</li>
</ul>


### Example Usage

<!-- UsageSnippet language="typescript" operationID="queryServiceHealthCheck" method="post" path="/query/api/v1/health-check/{model_type}" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
});

async function run() {
  const result = await pipeshub.queryService.healthCheck({
    scopedToken: process.env["PIPESHUB_SCOPED_TOKEN"] ?? "",
  }, {
    modelType: "llm",
    body: {
      provider: "<value>",
      configuration: {},
    },
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { queryServiceHealthCheck } from "pipeshub/funcs/query-service-health-check.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
});

async function run() {
  const res = await queryServiceHealthCheck(pipeshub, {
    scopedToken: process.env["PIPESHUB_SCOPED_TOKEN"] ?? "",
  }, {
    modelType: "llm",
    body: {
      provider: "<value>",
      configuration: {},
    },
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("queryServiceHealthCheck failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.QueryServiceHealthCheckRequest](../../models/operations/query-service-health-check-request.md)                                                                     | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `security`                                                                                                                                                                     | [operations.QueryServiceHealthCheckSecurity](../../models/operations/query-service-health-check-security.md)                                                                   | :heavy_check_mark:                                                                                                                                                             | The security requirements to use for the request.                                                                                                                              |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |
| `options.serverURL`                                                                                                                                                            | *string*                                                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                             | An optional server URL to use.                                                                                                                                                 |

### Response

**Promise\<[operations.QueryServiceHealthCheckResponse](../../models/operations/query-service-health-check-response.md)\>**

### Errors

| Error Type                                        | Status Code                                       | Content Type                                      |
| ------------------------------------------------- | ------------------------------------------------- | ------------------------------------------------- |
| errors.QueryServiceHealthCheckInternalServerError | 500                                               | application/json                                  |
| errors.PipeshubDefaultError                       | 4XX, 5XX                                          | \*/\*                                             |

## listTools

Retrieve all available tools that can be used by AI agents.<br><br>

<b>Service:</b> Query Service<br>
<b>Port:</b> 8000<br>
<b>Base URL:</b> <code>http://localhost:8000</code><br><br>

<b>Overview:</b><br>
Returns a list of tools registered in the system, including their parameters,
descriptions, and tags. Tools are loaded from ArangoDB.<br><br>

<b>Use Cases:</b><br>
<ul>
<li>Agent configuration UI - show available tools to assign to agents</li>
<li>Tool discovery for building custom agent workflows</li>
</ul>


### Example Usage

<!-- UsageSnippet language="typescript" operationID="queryListTools" method="get" path="/query/api/v1/tools" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.queryService.listTools();

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { queryServiceListTools } from "pipeshub/funcs/query-service-list-tools.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await queryServiceListTools(pipeshub);
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("queryServiceListTools failed:", res.error);
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
| `options.serverURL`                                                                                                                                                            | *string*                                                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                             | An optional server URL to use.                                                                                                                                                 |

### Response

**Promise\<[operations.QueryListToolsResponse[]](../../models/.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |