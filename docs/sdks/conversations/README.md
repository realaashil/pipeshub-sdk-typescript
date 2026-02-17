# Conversations

## Overview

AI-powered conversational chat management with citations and follow-up questions

### Available Operations

* [create](#create) - Create a new AI conversation
* [stream](#stream) - Create conversation with streaming response
* [list](#list) - List all conversations
* [listArchived](#listarchived) - List archived conversations
* [get](#get) - Get conversation by ID
* [delete](#delete) - Delete conversation
* [addMessage](#addmessage) - Add message to conversation
* [addMessageStream](#addmessagestream) - Add message with streaming response
* [share](#share) - Share conversation with users
* [unshare](#unshare) - Revoke conversation access
* [updateTitle](#updatetitle) - Update conversation title
* [patchArchive](#patcharchive) - Archive conversation
* [unarchive](#unarchive) - Unarchive conversation
* [regenerateAnswer](#regenerateanswer) - Regenerate AI response
* [updateMessageFeedback](#updatemessagefeedback) - Submit feedback on AI response

## create

Start a new conversation with PipesHub's AI assistant.<br><br>
<b>Overview:</b><br>
This endpoint creates a new conversation session and processes the initial query.
The AI searches your organization's knowledge bases for relevant information and
generates a response with citations to source documents.<br><br>
<b>How It Works:</b><br>
<ol>
<li>Your query is analyzed and converted to semantic embeddings</li>
<li>Relevant content is retrieved from indexed knowledge bases</li>
<li>The AI generates a response using the retrieved context</li>
<li>Citations link back to source documents for verification</li>
<li>Follow-up questions are suggested based on the conversation</li>
</ol>
<b>Filtering Options:</b><br>
<ul>
<li><b>recordIds:</b> Limit search to specific documents</li>
<li><b>filters.apps:</b> Search only specific connector apps</li>
<li><b>filters.kb:</b> Search only specific knowledge bases</li>
</ul>
<b>Model Selection:</b><br>
Use <code>modelKey</code> to select different AI models configured for your organization.
Each model may have different capabilities, speed, and accuracy trade-offs.


### Example Usage: filtered

<!-- UsageSnippet language="typescript" operationID="createConversation" method="post" path="/conversations/create" example="filtered" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.conversations.create({
    query: "Summarize the Q4 sales report",
    filters: {
      kb: [
        "550e8400-e29b-41d4-a716-446655440000",
      ],
    },
    modelKey: "gpt-4-turbo",
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { conversationsCreate } from "pipeshub/funcs/conversations-create.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await conversationsCreate(pipeshub, {
    query: "Summarize the Q4 sales report",
    filters: {
      kb: [
        "550e8400-e29b-41d4-a716-446655440000",
      ],
    },
    modelKey: "gpt-4-turbo",
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("conversationsCreate failed:", res.error);
  }
}

run();
```
### Example Usage: simple

<!-- UsageSnippet language="typescript" operationID="createConversation" method="post" path="/conversations/create" example="simple" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.conversations.create({
    query: "What is our company's vacation policy?",
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { conversationsCreate } from "pipeshub/funcs/conversations-create.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await conversationsCreate(pipeshub, {
    query: "What is our company's vacation policy?",
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("conversationsCreate failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [models.CreateConversationRequest](../../models/create-conversation-request.md)                                                                                                | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[models.Conversation](../../models/conversation.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## stream

Start a new conversation with real-time streaming response using Server-Sent Events (SSE).<br><br>
<b>Overview:</b><br>
This endpoint works like <code>/conversations/create</code> but streams the AI response
in real-time as it's generated, providing a more interactive user experience.<br><br>
<b>SSE Event Types:</b><br>
<ul>
<li><code>connected</code> - Connection established, processing started</li>
<li><code>chunk</code> - Partial response text (stream these to show typing effect)</li>
<li><code>citation</code> - Citation reference found during generation</li>
<li><code>complete</code> - Final message with full response, citations, and follow-up questions</li>
<li><code>error</code> - Error occurred during processing</li>
</ul>
<b>Client Implementation:</b><br>
<code>
const eventSource = new EventSource('/conversations/stream');<br>
eventSource.onmessage = (event) => {<br>
&nbsp;&nbsp;const data = JSON.parse(event.data);<br>
&nbsp;&nbsp;// Handle different event types<br>
};
</code><br><br>
<b>Error Handling:</b><br>
If an error occurs mid-stream, an <code>error</code> event is sent and the stream closes.
The conversation is marked as FAILED with the error reason stored.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="streamChat" method="post" path="/conversations/stream" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.conversations.stream({
    query: "What are the key findings from our Q4 financial report?",
    recordIds: [
      "507f1f77bcf86cd799439011",
      "507f1f77bcf86cd799439012",
    ],
    modelKey: "gpt-4-turbo",
    modelName: "GPT-4 Turbo",
    chatMode: "balanced",
  });

  for await (const event of result) {
    console.log(event);
  }
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { conversationsStream } from "pipeshub/funcs/conversations-stream.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await conversationsStream(pipeshub, {
    query: "What are the key findings from our Q4 financial report?",
    recordIds: [
      "507f1f77bcf86cd799439011",
      "507f1f77bcf86cd799439012",
    ],
    modelKey: "gpt-4-turbo",
    modelName: "GPT-4 Turbo",
    chatMode: "balanced",
  });
  if (res.ok) {
    const { value: result } = res;
    for await (const event of result) {
    console.log(event);
  }
  } else {
    console.log("conversationsStream failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [models.CreateConversationRequest](../../models/create-conversation-request.md)                                                                                                | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[EventStream<models.SSEEvent>](../../models/.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## list

Retrieve all conversations for the authenticated user.<br><br>
<b>Overview:</b><br>
Returns a list of all conversations owned by or shared with the current user.
Conversations are returned with their messages, status, and metadata.<br><br>
<b>Filtering:</b><br>
<ul>
<li>Only non-archived conversations are returned by default</li>
<li>Use <code>/conversations/show/archives</code> for archived conversations</li>
</ul>
<b>Sorting:</b><br>
Conversations are sorted by last activity timestamp (most recent first).


### Example Usage

<!-- UsageSnippet language="typescript" operationID="getAllConversations" method="get" path="/conversations" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.conversations.list();

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { conversationsList } from "pipeshub/funcs/conversations-list.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await conversationsList(pipeshub);
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("conversationsList failed:", res.error);
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

**Promise\<[models.Conversation[]](../../models/.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## listArchived

Retrieve all archived conversations for the authenticated user.<br><br>
<b>Overview:</b><br>
Archived conversations are hidden from the main list but preserved for reference.
This endpoint returns only conversations where <code>isArchived: true</code>.<br><br>
<b>Unarchiving:</b><br>
Use <code>PATCH /conversations/{id}/unarchive</code> to restore a conversation
to the active list.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="getArchivedConversations" method="get" path="/conversations/show/archives" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.conversations.listArchived();

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { conversationsListArchived } from "pipeshub/funcs/conversations-list-archived.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await conversationsListArchived(pipeshub);
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("conversationsListArchived failed:", res.error);
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

**Promise\<[models.Conversation[]](../../models/.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## get

Retrieve a specific conversation with its full message history.<br><br>
<b>Overview:</b><br>
Returns the complete conversation including all messages, citations,
feedback, and metadata. Messages can be paginated for long conversations.<br><br>
<b>Message Pagination:</b><br>
For conversations with many messages, use pagination parameters:
<ul>
<li><code>page</code>: Page number (default: 1)</li>
<li><code>limit</code>: Messages per page (default: 10)</li>
<li><code>sortBy</code>: Sort field (default: createdAt)</li>
<li><code>sortOrder</code>: 'asc' or 'desc' (default: desc)</li>
</ul>
<b>Access Control:</b><br>
Users can access conversations they own or that have been shared with them.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="getConversationById" method="get" path="/conversations/{conversationId}" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.conversations.get({
    conversationId: "507f1f77bcf86cd799439011",
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { conversationsGet } from "pipeshub/funcs/conversations-get.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await conversationsGet(pipeshub, {
    conversationId: "507f1f77bcf86cd799439011",
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("conversationsGet failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.GetConversationByIdRequest](../../models/operations/get-conversation-by-id-request.md)                                                                             | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.GetConversationByIdResponse](../../models/operations/get-conversation-by-id-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## delete

Delete a conversation by its ID.<br><br>
<b>Overview:</b><br>
Performs a soft delete by setting <code>isDeleted: true</code>.
The conversation is removed from listings but preserved in the database.<br><br>
<b>Permissions:</b><br>
Only the conversation owner (initiator) can delete it.
Shared users cannot delete conversations.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="deleteConversationById" method="delete" path="/conversations/{conversationId}" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.conversations.delete({
    conversationId: "<value>",
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { conversationsDelete } from "pipeshub/funcs/conversations-delete.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await conversationsDelete(pipeshub, {
    conversationId: "<value>",
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("conversationsDelete failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.DeleteConversationByIdRequest](../../models/operations/delete-conversation-by-id-request.md)                                                                       | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.DeleteConversationByIdResponse](../../models/operations/delete-conversation-by-id-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## addMessage

Add a follow-up message to an existing conversation.<br><br>
<b>Overview:</b><br>
Continues an existing conversation by adding a new user query.
The AI maintains context from previous messages when generating the response.<br><br>
<b>Context Handling:</b><br>
<ul>
<li>Previous messages provide context for the new query</li>
<li>Citations from earlier messages may be referenced</li>
<li>The AI can refer back to previous topics discussed</li>
</ul>
<b>Model Override:</b><br>
You can specify a different model for this message using <code>modelKey</code>.
This allows switching models mid-conversation if needed.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="addMessage" method="post" path="/conversations/{conversationId}/messages" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.conversations.addMessage({
    conversationId: "<value>",
    body: {
      query: "Can you elaborate on the revenue trends?",
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
import { conversationsAddMessage } from "pipeshub/funcs/conversations-add-message.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await conversationsAddMessage(pipeshub, {
    conversationId: "<value>",
    body: {
      query: "Can you elaborate on the revenue trends?",
    },
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("conversationsAddMessage failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.AddMessageRequest](../../models/operations/add-message-request.md)                                                                                                 | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[models.Conversation](../../models/conversation.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## addMessageStream

Add a follow-up message to an existing conversation with real-time SSE streaming.<br><br>
<b>Overview:</b><br>
Same as <code>POST /conversations/{id}/messages</code> but with streaming response.
Provides real-time feedback as the AI generates its response.<br><br>
<b>SSE Events:</b><br>
See <code>/conversations/stream</code> for event type documentation.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="addMessageStream" method="post" path="/conversations/{conversationId}/messages/stream" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.conversations.addMessageStream({
    conversationId: "<value>",
    body: {
      query: "Can you elaborate on the revenue trends?",
    },
  });

  for await (const event of result) {
    console.log(event);
  }
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { conversationsAddMessageStream } from "pipeshub/funcs/conversations-add-message-stream.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await conversationsAddMessageStream(pipeshub, {
    conversationId: "<value>",
    body: {
      query: "Can you elaborate on the revenue trends?",
    },
  });
  if (res.ok) {
    const { value: result } = res;
    for await (const event of result) {
    console.log(event);
  }
  } else {
    console.log("conversationsAddMessageStream failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.AddMessageStreamRequest](../../models/operations/add-message-stream-request.md)                                                                                    | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[EventStream<models.SSEEvent>](../../models/.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## share

Share a conversation with other users in your organization.<br><br>
<b>Overview:</b><br>
Allows the conversation owner to grant access to other users.
Shared users can view the conversation and optionally add messages.<br><br>
<b>Access Levels:</b><br>
<ul>
<li><code>read</code> - Can view conversation and messages (default)</li>
<li><code>write</code> - Can view and add new messages</li>
</ul>
<b>Permissions:</b><br>
Only the conversation initiator (owner) can share. Users must belong
to the same organization.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="shareConversation" method="post" path="/conversations/{conversationId}/share" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.conversations.share({
    conversationId: "<value>",
    body: {
      userIds: [
        "507f1f77bcf86cd799439011",
      ],
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
import { conversationsShare } from "pipeshub/funcs/conversations-share.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await conversationsShare(pipeshub, {
    conversationId: "<value>",
    body: {
      userIds: [
        "507f1f77bcf86cd799439011",
      ],
    },
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("conversationsShare failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.ShareConversationRequest](../../models/operations/share-conversation-request.md)                                                                                   | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[models.Conversation](../../models/conversation.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## unshare

Remove sharing access from users.<br><br>
<b>Overview:</b><br>
Removes specified users from the conversation's sharedWith list.
Those users will no longer be able to access the conversation.<br><br>
<b>Permissions:</b><br>
Only the conversation owner can revoke access.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="unshareConversation" method="post" path="/conversations/{conversationId}/unshare" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.conversations.unshare({
    conversationId: "<value>",
    body: {
      userIds: [
        "<value 1>",
        "<value 2>",
      ],
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
import { conversationsUnshare } from "pipeshub/funcs/conversations-unshare.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await conversationsUnshare(pipeshub, {
    conversationId: "<value>",
    body: {
      userIds: [
        "<value 1>",
        "<value 2>",
      ],
    },
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("conversationsUnshare failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.UnshareConversationRequest](../../models/operations/unshare-conversation-request.md)                                                                               | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[models.Conversation](../../models/conversation.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## updateTitle

Update the title of a conversation.<br><br>
<b>Overview:</b><br>
Conversation titles are auto-generated from the first query by default.
Use this endpoint to set a custom, more descriptive title.<br><br>
<b>Title Limits:</b><br>
<ul>
<li>Minimum: 1 character</li>
<li>Maximum: 200 characters</li>
</ul>


### Example Usage

<!-- UsageSnippet language="typescript" operationID="updateConversationTitle" method="patch" path="/conversations/{conversationId}/title" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.conversations.updateTitle({
    conversationId: "<value>",
    body: {
      title: "Q4 Sales Analysis Discussion",
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
import { conversationsUpdateTitle } from "pipeshub/funcs/conversations-update-title.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await conversationsUpdateTitle(pipeshub, {
    conversationId: "<value>",
    body: {
      title: "Q4 Sales Analysis Discussion",
    },
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("conversationsUpdateTitle failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.UpdateConversationTitleRequest](../../models/operations/update-conversation-title-request.md)                                                                      | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[models.Conversation](../../models/conversation.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## patchArchive

Archive a conversation to hide it from the main list.<br><br>
<b>Overview:</b><br>
Archived conversations are preserved but hidden from the default conversation list.
Use archiving to clean up your workspace without permanently deleting conversations.<br><br>
<b>Retrieval:</b><br>
View archived conversations using <code>GET /conversations/show/archives</code>.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="archiveConversation" method="patch" path="/conversations/{conversationId}/archive" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.conversations.patchArchive({
    conversationId: "<value>",
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { conversationsPatchArchive } from "pipeshub/funcs/conversations-patch-archive.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await conversationsPatchArchive(pipeshub, {
    conversationId: "<value>",
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("conversationsPatchArchive failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.ArchiveConversationRequest](../../models/operations/archive-conversation-request.md)                                                                               | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[models.Conversation](../../models/conversation.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## unarchive

Restore an archived conversation to the active list.<br><br>
<b>Overview:</b><br>
Removes the archived flag, making the conversation visible in the main list again.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="unarchiveConversation" method="patch" path="/conversations/{conversationId}/unarchive" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.conversations.unarchive({
    conversationId: "<value>",
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { conversationsUnarchive } from "pipeshub/funcs/conversations-unarchive.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await conversationsUnarchive(pipeshub, {
    conversationId: "<value>",
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("conversationsUnarchive failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.UnarchiveConversationRequest](../../models/operations/unarchive-conversation-request.md)                                                                           | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[models.Conversation](../../models/conversation.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## regenerateAnswer

Regenerate the AI response for a specific message.<br><br>
<b>Overview:</b><br>
If you're not satisfied with an AI response, use this endpoint to generate
a new answer. The AI will re-process the original query and may produce
a different response.<br><br>
<b>Use Cases:</b><br>
<ul>
<li>Response was incomplete or unclear</li>
<li>Want to try a different AI model</li>
<li>New documents have been indexed since original response</li>
</ul>
<b>Model Override:</b><br>
Specify <code>modelKey</code> to use a different model for regeneration.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="regenerateAnswer" method="post" path="/conversations/{conversationId}/message/{messageId}/regenerate" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.conversations.regenerateAnswer({
    conversationId: "<value>",
    messageId: "<value>",
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { conversationsRegenerateAnswer } from "pipeshub/funcs/conversations-regenerate-answer.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await conversationsRegenerateAnswer(pipeshub, {
    conversationId: "<value>",
    messageId: "<value>",
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("conversationsRegenerateAnswer failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.RegenerateAnswerRequest](../../models/operations/regenerate-answer-request.md)                                                                                     | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[models.Conversation](../../models/conversation.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## updateMessageFeedback

Provide feedback on an AI-generated response.<br><br>
<b>Overview:</b><br>
Feedback helps improve AI response quality over time. You can rate
various aspects of the response and provide detailed comments.<br><br>
<b>Feedback Options:</b><br>
<ul>
<li><b>isHelpful:</b> Overall thumbs up/down</li>
<li><b>ratings:</b> 1-5 scale for accuracy, relevance, completeness, clarity</li>
<li><b>categories:</b> Issue categories (incorrect info, too verbose, etc.)</li>
<li><b>comments:</b> Free-text positive/negative feedback and suggestions</li>
<li><b>citationFeedback:</b> Rate individual citations</li>
</ul>
<b>Restrictions:</b><br>
Feedback can only be submitted on <code>bot_response</code> messages,
not on user queries or system messages.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="updateMessageFeedback" method="post" path="/conversations/{conversationId}/message/{messageId}/feedback" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.conversations.updateMessageFeedback({
    conversationId: "<value>",
    messageId: "<value>",
    body: {},
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { conversationsUpdateMessageFeedback } from "pipeshub/funcs/conversations-update-message-feedback.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await conversationsUpdateMessageFeedback(pipeshub, {
    conversationId: "<value>",
    messageId: "<value>",
    body: {},
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("conversationsUpdateMessageFeedback failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.UpdateMessageFeedbackRequest](../../models/operations/update-message-feedback-request.md)                                                                          | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[models.Conversation](../../models/conversation.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |