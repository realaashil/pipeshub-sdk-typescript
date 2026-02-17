# Users

## Overview

User management operations

### Available Operations

* [get](#get) - Get all users
* [create](#create) - Create a new user
* [getById](#getbyid) - Get user by ID
* [update](#update) - Update user
* [delete](#delete) - Delete user
* [fetchWithGroups](#fetchwithgroups) - Get all users with their groups
* [getEmail](#getemail) - Get user email by ID
* [getByIds](#getbyids) - Get users by IDs (bulk)
* [checkExistsByEmail](#checkexistsbyemail) - Check if user exists by email
* [getInternal](#getinternal) - Get user (internal service-to-service)
* [updateFullName](#updatefullname) - Update user full name
* [updateFirstName](#updatefirstname) - Update user first name
* [updateLastName](#updatelastname) - Update user last name
* [updateDesignation](#updatedesignation) - Update user designation
* [checkIsAdmin](#checkisadmin) - Check if user is admin
* [uploadDisplayPicture](#uploaddisplaypicture) - Upload display picture
* [getDisplayPicture](#getdisplaypicture) - Get display picture
* [removeDisplayPicture](#removedisplaypicture) - Remove display picture
* [bulkInvite](#bulkinvite) - Bulk invite users
* [resendInvite](#resendinvite) - Resend user invite
* [listGraph](#listgraph) - List users (paginated with graph data)
* [listTeams](#listteams) - Get current user's teams

## get

Retrieve a paginated list of all users in the organization.<br><br>
<b>Overview:</b><br>
This endpoint returns all active users in your organization. It's the primary endpoint for listing and displaying users in admin dashboards, user directories, and selection interfaces.<br><br>
<b>Response Data:</b><br>
<ul>
<li>User profile information (name, email, designation)</li>
<li>Account status (active, pending invitation, disabled)</li>
<li>Login history (hasLoggedIn flag)</li>
<li>Timestamps (createdAt, updatedAt)</li>
</ul>
<b>Privacy Controls:</b><br>
<ul>
<li>Email addresses may be masked based on organization settings</li>
<li>Sensitive fields (password, tokens) are never exposed</li>
<li>Deleted users are excluded from results</li>
</ul>
<b>Performance Notes:</b><br>
<ul>
<li>Results are cached for improved performance</li>
<li>For large organizations, consider using pagination</li>
<li>Use <code>/users/by-ids</code> for fetching specific users</li>
</ul>


### Example Usage

<!-- UsageSnippet language="typescript" operationID="getAllUsers" method="get" path="/users" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.users.get({});

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { usersGet } from "pipeshub/funcs/users-get.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await usersGet(pipeshub, {});
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("usersGet failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.GetAllUsersRequest](../../models/operations/get-all-users-request.md)                                                                                              | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.GetAllUsersResponse](../../models/operations/get-all-users-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## create

Create a new user account in the organization and optionally send an invitation email.<br><br>
<b>Overview:</b><br>
This endpoint creates a new user account. The user will be added to the organization but won't have a password set until they complete the invitation flow or are assigned one by an admin.<br><br>
<b>Invitation Flow:</b><br>
<ol>
<li>Admin creates user with this endpoint</li>
<li>System generates invitation token</li>
<li>User receives invitation email (if sendInvite is true)</li>
<li>User clicks link and sets their password</li>
<li>User can now log in normally</li>
</ol>
<b>Validation Rules:</b><br>
<ul>
<li><code>fullName</code>: Required, 1-100 characters</li>
<li><code>email</code>: Required, valid email format, must be unique in org</li>
<li><code>mobile</code>: Optional, format: +[country][number] (10-15 digits)</li>
<li><code>designation</code>: Optional, job title or role</li>
</ul>
<b>Side Effects:</b><br>
<ul>
<li>User is automatically added to the "everyone" group</li>
<li>Invitation email sent if <code>sendInvite: true</code></li>
<li>User creation event published to event bus</li>
<li>Audit log entry created</li>
</ul>
<b>Authorization:</b><br>
Only organization administrators can create new users.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="createUser" method="post" path="/users" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.users.create({
    fullName: "John Smith",
    email: "john.smith@company.com",
    mobile: "+15551234567",
    designation: "Software Engineer",
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { usersCreate } from "pipeshub/funcs/users-create.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await usersCreate(pipeshub, {
    fullName: "John Smith",
    email: "john.smith@company.com",
    mobile: "+15551234567",
    designation: "Software Engineer",
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("usersCreate failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.CreateUserRequest](../../models/operations/create-user-request.md)                                                                                                 | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.CreateUserResponse](../../models/operations/create-user-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## getById

Retrieve detailed information about a specific user by their unique identifier.<br><br>
<b>Overview:</b><br>
This endpoint returns the complete user profile for the specified user ID. Use this to display user details in profiles, settings pages, or when you need full user information.<br><br>
<b>Response Data:</b><br>
<ul>
<li>Basic info: fullName, firstName, lastName, email</li>
<li>Contact: mobile, address</li>
<li>Professional: designation</li>
<li>Status: hasLoggedIn, isDeleted, accountStatus</li>
<li>Metadata: createdAt, updatedAt, createdBy</li>
</ul>
<b>Privacy Notes:</b><br>
<ul>
<li>Email may be masked for non-admin users based on org settings</li>
<li>Password and sensitive tokens are never returned</li>
<li>Display picture URL returned if set</li>
</ul>
<b>Related Endpoints:</b><br>
<ul>
<li><code>GET /users/{id}/email</code> - Get just the email (admin only)</li>
<li><code>GET /users/fetch/with-groups</code> - Get user with group memberships</li>
</ul>


### Example Usage

<!-- UsageSnippet language="typescript" operationID="getUserById" method="get" path="/users/{id}" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.users.getById({
    id: "507f1f77bcf86cd799439011",
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { usersGetById } from "pipeshub/funcs/users-get-by-id.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await usersGetById(pipeshub, {
    id: "507f1f77bcf86cd799439011",
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("usersGetById failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.GetUserByIdRequest](../../models/operations/get-user-by-id-request.md)                                                                                             | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.GetUserByIdResponse](../../models/operations/get-user-by-id-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## update

Update user profile information. Users can update their own profile, admins can update any user.<br><br>
<b>Overview:</b><br>
This endpoint allows updating user profile fields. The scope of allowed updates depends on the requester's role and relationship to the user being updated.<br><br>
<b>Authorization Matrix:</b><br>
<ul>
<li><b>Self-update:</b> Users can update their own fullName, mobile, designation, address</li>
<li><b>Admin-update:</b> Admins can update any field for any user</li>
<li><b>Email changes:</b> Require admin privileges and trigger re-verification</li>
</ul>
<b>Updatable Fields:</b><br>
<ul>
<li><code>fullName</code>: Display name (also updates firstName/lastName if parsed)</li>
<li><code>firstName</code>: First name only</li>
<li><code>lastName</code>: Last name only</li>
<li><code>email</code>: Email address (admin only, triggers verification)</li>
<li><code>mobile</code>: Phone number with country code</li>
<li><code>designation</code>: Job title</li>
<li><code>address</code>: Full address object</li>
</ul>
<b>Validation Rules:</b><br>
<ul>
<li>Email must be unique within the organization</li>
<li>Mobile must match pattern: +[country][number]</li>
<li>Name fields: 1-100 characters</li>
</ul>
<b>Side Effects:</b><br>
<ul>
<li>User update event published to event bus</li>
<li>Audit log entry created for admin updates</li>
<li>Email change triggers verification email</li>
</ul>


### Example Usage

<!-- UsageSnippet language="typescript" operationID="updateUser" method="put" path="/users/{id}" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.users.update({
    id: "507f1f77bcf86cd799439011",
    body: {
      fullName: "John Smith",
      firstName: "John",
      lastName: "Smith",
      email: "john.smith@company.com",
      mobile: "+15551234567",
      designation: "Senior Software Engineer",
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
import { usersUpdate } from "pipeshub/funcs/users-update.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await usersUpdate(pipeshub, {
    id: "507f1f77bcf86cd799439011",
    body: {
      fullName: "John Smith",
      firstName: "John",
      lastName: "Smith",
      email: "john.smith@company.com",
      mobile: "+15551234567",
      designation: "Senior Software Engineer",
    },
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("usersUpdate failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.UpdateUserRequest](../../models/operations/update-user-request.md)                                                                                                 | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.UpdateUserResponse](../../models/operations/update-user-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## delete

Soft delete a user from the organization. The user account is deactivated but data is retained for audit purposes.<br><br>
<b>Overview:</b><br>
This endpoint performs a soft delete on a user account. The user is marked as deleted and can no longer access the system, but their data is retained for compliance and audit purposes.<br><br>
<b>What Happens on Delete:</b><br>
<ol>
<li>User's <code>isDeleted</code> flag is set to true</li>
<li>User's password is cleared</li>
<li>User is removed from all user groups</li>
<li>User's active sessions are invalidated</li>
<li>User deletion event is published</li>
</ol>
<b>Restrictions:</b><br>
<ul>
<li>Cannot delete organization admins (demote first)</li>
<li>Cannot delete the organization owner</li>
<li>Cannot delete yourself through this endpoint</li>
<li>Cannot delete already-deleted users</li>
</ul>
<b>Data Retention:</b><br>
<ul>
<li>User profile data is retained (soft delete)</li>
<li>User's documents and content remain with updated ownership</li>
<li>Audit logs are preserved</li>
<li>Data can be permanently purged by super admin if required</li>
</ul>
<b>Recovery:</b><br>
Deleted users can be restored by organization admins within a configurable retention period.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="deleteUser" method="delete" path="/users/{id}" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.users.delete({
    id: "507f1f77bcf86cd799439011",
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { usersDelete } from "pipeshub/funcs/users-delete.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await usersDelete(pipeshub, {
    id: "507f1f77bcf86cd799439011",
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("usersDelete failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.DeleteUserRequest](../../models/operations/delete-user-request.md)                                                                                                 | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.DeleteUserResponse](../../models/operations/delete-user-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## fetchWithGroups

Retrieve all users along with their group memberships in a single optimized query.<br><br>
<b>Overview:</b><br>
This endpoint returns users with their associated groups pre-loaded, eliminating the need for separate group lookup calls. Ideal for admin dashboards that need to display user permissions at a glance.<br><br>
<b>Use Cases:</b><br>
<ul>
<li>Admin dashboards showing user-group matrix</li>
<li>Permission auditing and compliance checks</li>
<li>Bulk user management interfaces</li>
<li>Access control visualization</li>
</ul>
<b>Response Data per User:</b><br>
<ul>
<li><code>_id</code>: User's unique identifier</li>
<li><code>userId</code>: User's public-facing ID</li>
<li><code>orgId</code>: Organization identifier</li>
<li><code>fullName</code>: User's display name</li>
<li><code>hasLoggedIn</code>: Whether user has ever logged in</li>
<li><code>groups</code>: Array of group objects with name and type</li>
</ul>
<b>Group Types Returned:</b><br>
<ul>
<li><code>admin</code>: Administrative groups with elevated permissions</li>
<li><code>standard</code>: Regular user groups</li>
<li><code>everyone</code>: Default group containing all org users</li>
<li><code>custom</code>: Custom groups created by admins</li>
</ul>
<b>Performance Notes:</b><br>
Uses aggregation pipeline for efficient single-query retrieval. Cached results for improved performance on large organizations.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="getAllUsersWithGroups" method="get" path="/users/fetch/with-groups" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.users.fetchWithGroups({});

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { usersFetchWithGroups } from "pipeshub/funcs/users-fetch-with-groups.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await usersFetchWithGroups(pipeshub, {});
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("usersFetchWithGroups failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.GetAllUsersWithGroupsRequest](../../models/operations/get-all-users-with-groups-request.md)                                                                        | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.GetAllUsersWithGroupsResponse](../../models/operations/get-all-users-with-groups-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## getEmail

Retrieve the email address for a specific user. This is a dedicated endpoint for email lookup with proper access controls.<br><br>
<b>Overview:</b><br>
This endpoint provides direct access to a user's email address. It exists separately from the main user endpoint to allow granular permission control over email visibility.<br><br>
<b>Use Cases:</b><br>
<ul>
<li>Admin communication workflows</li>
<li>Invitation and notification systems</li>
<li>Email-based user lookup</li>
<li>Contact information export</li>
</ul>
<b>Privacy Considerations:</b><br>
<ul>
<li>Only organization admins can access this endpoint</li>
<li>Access is logged for audit purposes</li>
<li>Consider GDPR/privacy regulations when exposing emails</li>
</ul>
<b>Authorization:</b><br>
Requires admin privileges. Regular users should use the main user endpoint which may mask emails based on organization settings.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="getUserEmailById" method="get" path="/users/{id}/email" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.users.getEmail({
    id: "507f1f77bcf86cd799439011",
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { usersGetEmail } from "pipeshub/funcs/users-get-email.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await usersGetEmail(pipeshub, {
    id: "507f1f77bcf86cd799439011",
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("usersGetEmail failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.GetUserEmailByIdRequest](../../models/operations/get-user-email-by-id-request.md)                                                                                  | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.GetUserEmailByIdResponse](../../models/operations/get-user-email-by-id-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## getByIds

Retrieve multiple users by their IDs in a single optimized request. Ideal for efficiently fetching a specific set of users.<br><br>
<b>Overview:</b><br>
This bulk endpoint allows fetching multiple users in a single API call, reducing network overhead when you need to display information about several known users.<br><br>
<b>Use Cases:</b><br>
<ul>
<li>Fetching user details for a list of team members</li>
<li>Populating user cards in a dashboard</li>
<li>Loading participants in a document or conversation</li>
<li>Building user mention/autocomplete features</li>
</ul>
<b>Request Format:</b><br>
<ul>
<li>Send array of user IDs in request body</li>
<li>Each ID must be valid 24-character MongoDB ObjectId</li>
<li>Maximum 100 IDs per request (for performance)</li>
<li>Duplicate IDs are automatically deduplicated</li>
</ul>
<b>Response Behavior:</b><br>
<ul>
<li>Returns array of found users</li>
<li>Order matches order of requested IDs</li>
<li>Non-existent or deleted users are silently omitted</li>
<li>Partial results returned if some IDs are invalid</li>
</ul>
<b>Performance Notes:</b><br>
Uses single database query with $in operator for optimal performance. Preferable to multiple individual user fetches.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="getUsersByIds" method="post" path="/users/by-ids" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.users.getByIds({
    userIds: [
      "507f1f77bcf86cd799439011",
      "507f1f77bcf86cd799439012",
    ],
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { usersGetByIds } from "pipeshub/funcs/users-get-by-ids.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await usersGetByIds(pipeshub, {
    userIds: [
      "507f1f77bcf86cd799439011",
      "507f1f77bcf86cd799439012",
    ],
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("usersGetByIds failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.GetUsersByIdsRequest](../../models/operations/get-users-by-ids-request.md)                                                                                         | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.GetUsersByIdsResponse](../../models/operations/get-users-by-ids-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## checkExistsByEmail

Check if a user account exists with the given email address. Used for pre-validation in registration and invitation flows.<br><br>
<b>Overview:</b><br>
This internal service endpoint validates email existence before creating accounts or sending invitations. It helps prevent duplicate accounts and validates recovery email addresses.<br><br>
<b>Use Cases:</b><br>
<ul>
<li>Pre-flight check before user invitation</li>
<li>Email validation during registration</li>
<li>Account recovery flow validation</li>
<li>Duplicate prevention checks</li>
</ul>
<b>Security Model:</b><br>
<ul>
<li>Requires scoped token with USER_LOOKUP privilege</li>
<li>Not accessible with regular bearer tokens</li>
<li>Typically called from internal services only</li>
</ul>
<b>Response Behavior:</b><br>
<ul>
<li>Returns matching users (including soft-deleted for recovery)</li>
<li>Empty array if no match found</li>
<li>Does not expose whether email exists to prevent enumeration</li>
</ul>
<b>Note:</b> May return soft-deleted users to support account recovery workflows.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="checkUserExistsByEmail" method="get" path="/users/email/exists" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
});

async function run() {
  const result = await pipeshub.users.checkExistsByEmail({
    scopedToken: process.env["PIPESHUB_SCOPED_TOKEN"] ?? "",
  }, {
    email: "john.smith@company.com",
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { usersCheckExistsByEmail } from "pipeshub/funcs/users-check-exists-by-email.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
});

async function run() {
  const res = await usersCheckExistsByEmail(pipeshub, {
    scopedToken: process.env["PIPESHUB_SCOPED_TOKEN"] ?? "",
  }, {
    email: "john.smith@company.com",
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("usersCheckExistsByEmail failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.CheckUserExistsByEmailRequest](../../models/operations/check-user-exists-by-email-request.md)                                                                      | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `security`                                                                                                                                                                     | [operations.CheckUserExistsByEmailSecurity](../../models/operations/check-user-exists-by-email-security.md)                                                                    | :heavy_check_mark:                                                                                                                                                             | The security requirements to use for the request.                                                                                                                              |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.CheckUserExistsByEmailResponse](../../models/operations/check-user-exists-by-email-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## getInternal

Internal endpoint for service-to-service user lookup. Returns complete user data without privacy masking.<br><br>
<b>Overview:</b><br>
This internal endpoint provides full user data access for trusted backend services. Unlike public endpoints, it bypasses privacy controls and returns complete user information.<br><br>
<b>Security Model:</b><br>
<ul>
<li>Requires scoped token with USER_LOOKUP privilege</li>
<li>Not accessible via regular bearer tokens</li>
<li>Intended for trusted internal services only</li>
<li>All access is logged for audit purposes</li>
</ul>
<b>Intended Consumers:</b><br>
<ul>
<li>Email notification service</li>
<li>Analytics and reporting services</li>
<li>Audit logging service</li>
<li>Integration sync services</li>
</ul>
<b>Data Returned:</b><br>
Complete user object including fields that may be masked in public endpoints (email, phone, etc.).<br><br>
<b>Warning:</b><br>
This endpoint returns sensitive data. Ensure consuming services handle data according to privacy policies.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="getInternalUser" method="get" path="/users/internal/{id}" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
});

async function run() {
  const result = await pipeshub.users.getInternal({
    scopedToken: process.env["PIPESHUB_SCOPED_TOKEN"] ?? "",
  }, {
    id: "507f1f77bcf86cd799439011",
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { usersGetInternal } from "pipeshub/funcs/users-get-internal.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
});

async function run() {
  const res = await usersGetInternal(pipeshub, {
    scopedToken: process.env["PIPESHUB_SCOPED_TOKEN"] ?? "",
  }, {
    id: "507f1f77bcf86cd799439011",
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("usersGetInternal failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.GetInternalUserRequest](../../models/operations/get-internal-user-request.md)                                                                                      | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `security`                                                                                                                                                                     | [operations.GetInternalUserSecurity](../../models/operations/get-internal-user-security.md)                                                                                    | :heavy_check_mark:                                                                                                                                                             | The security requirements to use for the request.                                                                                                                              |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.GetInternalUserResponse](../../models/operations/get-internal-user-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## updateFullName

Update the full name of a user. This is a targeted update endpoint for changing only the display name without affecting other profile fields.<br><br>
<b>Overview:</b><br>
This endpoint updates a user's fullName field, which is their primary display name throughout the application. The firstName and lastName fields may also be updated based on name parsing logic.<br><br>
<b>Authorization:</b><br>
<ul>
<li><b>Self-update:</b> Users can update their own full name</li>
<li><b>Admin-update:</b> Admins can update any user's name</li>
</ul>
<b>Side Effects:</b><br>
<ul>
<li>Updates fullName field</li>
<li>May parse and update firstName/lastName</li>
<li>User update event published</li>
<li>Cached user data invalidated</li>
</ul>
<b>Use Cases:</b><br>
<ul>
<li>User profile name change</li>
<li>Name correction by admin</li>
<li>Legal name update</li>
</ul>


### Example Usage

<!-- UsageSnippet language="typescript" operationID="updateUserFullName" method="patch" path="/users/{id}/fullname" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.users.updateFullName({
    id: "<id>",
    body: {
      fullName: "Jim Denesik",
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
import { usersUpdateFullName } from "pipeshub/funcs/users-update-full-name.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await usersUpdateFullName(pipeshub, {
    id: "<id>",
    body: {
      fullName: "Jim Denesik",
    },
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("usersUpdateFullName failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.UpdateUserFullNameRequest](../../models/operations/update-user-full-name-request.md)                                                                               | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[models.User](../../models/user.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## updateFirstName

Update only the first name of a user without affecting other profile fields.<br><br>
<b>Overview:</b><br>
This targeted endpoint updates just the firstName field. Useful when you need fine-grained control over name components rather than updating the full name.<br><br>
<b>Authorization:</b><br>
<ul>
<li><b>Self-update:</b> Users can update their own first name</li>
<li><b>Admin-update:</b> Admins can update any user's first name</li>
</ul>
<b>Note:</b> This does NOT automatically update the fullName field. Use <code>/users/{id}/fullname</code> if you need to update the complete display name.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="updateUserFirstName" method="patch" path="/users/{id}/firstName" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.users.updateFirstName({
    id: "507f1f77bcf86cd799439011",
    body: {
      firstName: "John",
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
import { usersUpdateFirstName } from "pipeshub/funcs/users-update-first-name.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await usersUpdateFirstName(pipeshub, {
    id: "507f1f77bcf86cd799439011",
    body: {
      firstName: "John",
    },
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("usersUpdateFirstName failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.UpdateUserFirstNameRequest](../../models/operations/update-user-first-name-request.md)                                                                             | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.UpdateUserFirstNameResponse](../../models/operations/update-user-first-name-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## updateLastName

Update only the last name of a user without affecting other profile fields.<br><br>
<b>Overview:</b><br>
This targeted endpoint updates just the lastName field. Useful for fine-grained control over name components.<br><br>
<b>Authorization:</b><br>
<ul>
<li><b>Self-update:</b> Users can update their own last name</li>
<li><b>Admin-update:</b> Admins can update any user's last name</li>
</ul>
<b>Note:</b> This does NOT automatically update the fullName field. Use <code>/users/{id}/fullname</code> if you need to update the complete display name.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="updateUserLastName" method="patch" path="/users/{id}/lastName" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.users.updateLastName({
    id: "507f1f77bcf86cd799439011",
    body: {
      lastName: "Smith",
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
import { usersUpdateLastName } from "pipeshub/funcs/users-update-last-name.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await usersUpdateLastName(pipeshub, {
    id: "507f1f77bcf86cd799439011",
    body: {
      lastName: "Smith",
    },
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("usersUpdateLastName failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.UpdateUserLastNameRequest](../../models/operations/update-user-last-name-request.md)                                                                               | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.UpdateUserLastNameResponse](../../models/operations/update-user-last-name-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## updateDesignation

Update the job title or designation of a user.<br><br>
<b>Overview:</b><br>
This endpoint updates the user's designation field, which typically represents their job title, role, or position within the organization.<br><br>
<b>Authorization:</b><br>
<ul>
<li><b>Self-update:</b> Users can update their own designation</li>
<li><b>Admin-update:</b> Admins can update any user's designation</li>
</ul>
<b>Common Values:</b><br>
<ul>
<li>Software Engineer</li>
<li>Product Manager</li>
<li>Team Lead</li>
<li>Director of Engineering</li>
</ul>
<b>Display:</b><br>
Designation is shown in user profiles, team views, and organizational charts.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="updateUserDesignation" method="patch" path="/users/{id}/designation" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.users.updateDesignation({
    id: "507f1f77bcf86cd799439011",
    body: {
      designation: "Senior Software Engineer",
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
import { usersUpdateDesignation } from "pipeshub/funcs/users-update-designation.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await usersUpdateDesignation(pipeshub, {
    id: "507f1f77bcf86cd799439011",
    body: {
      designation: "Senior Software Engineer",
    },
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("usersUpdateDesignation failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.UpdateUserDesignationRequest](../../models/operations/update-user-designation-request.md)                                                                          | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.UpdateUserDesignationResponse](../../models/operations/update-user-designation-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## checkIsAdmin

Verify whether a specific user has administrative privileges in the organization.<br><br>
<b>Overview:</b><br>
This endpoint checks if the specified user belongs to an admin group and has elevated permissions. It's useful for authorization checks before performing admin-only operations.<br><br>
<b>What Makes a User an Admin:</b><br>
<ul>
<li>Member of a group with type "admin"</li>
<li>Has explicit admin role assignment</li>
<li>Organization owner (always admin)</li>
</ul>
<b>Use Cases:</b><br>
<ul>
<li>UI permission checks before showing admin features</li>
<li>Pre-flight authorization validation</li>
<li>Access control for sensitive operations</li>
</ul>
<b>Response Codes:</b><br>
<ul>
<li><code>200</code>: User IS an admin</li>
<li><code>403</code>: User is NOT an admin</li>
</ul>


### Example Usage

<!-- UsageSnippet language="typescript" operationID="checkUserIsAdmin" method="get" path="/users/{id}/adminCheck" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.users.checkIsAdmin({
    id: "507f1f77bcf86cd799439011",
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { usersCheckIsAdmin } from "pipeshub/funcs/users-check-is-admin.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await usersCheckIsAdmin(pipeshub, {
    id: "507f1f77bcf86cd799439011",
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("usersCheckIsAdmin failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.CheckUserIsAdminRequest](../../models/operations/check-user-is-admin-request.md)                                                                                   | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.CheckUserIsAdminResponse](../../models/operations/check-user-is-admin-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## uploadDisplayPicture

Upload or update the display picture (avatar) for the authenticated user.<br><br>
<b>Overview:</b><br>
This endpoint allows users to upload their profile picture. The image is processed, resized, and stored for use throughout the application.<br><br>
<b>File Requirements:</b><br>
<ul>
<li><b>Allowed types:</b> PNG, JPEG, JPG, WebP, GIF</li>
<li><b>Maximum size:</b> 1MB (1,048,576 bytes)</li>
<li><b>Recommended dimensions:</b> 256x256 pixels or larger</li>
<li><b>Aspect ratio:</b> Square recommended (will be cropped to square)</li>
</ul>
<b>Image Processing:</b><br>
<ul>
<li>Images are automatically resized to standard dimensions</li>
<li>Converted to JPEG for consistency and smaller file size</li>
<li>Multiple sizes may be generated (thumbnail, standard, large)</li>
<li>Original is not preserved</li>
</ul>
<b>Side Effects:</b><br>
<ul>
<li>Previous display picture is replaced</li>
<li>Cached images are invalidated</li>
<li>CDN cache may take time to update</li>
</ul>
<b>Authorization:</b><br>
Users can only upload their own display picture. Admins cannot upload on behalf of other users.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="uploadUserDisplayPicture" method="put" path="/users/dp" -->
```typescript
import { openAsBlob } from "node:fs";
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.users.uploadDisplayPicture({
    file: await openAsBlob("example.file"),
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { openAsBlob } from "node:fs";
import { PipeshubCore } from "pipeshub/core.js";
import { usersUploadDisplayPicture } from "pipeshub/funcs/users-upload-display-picture.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await usersUploadDisplayPicture(pipeshub, {
    file: await openAsBlob("example.file"),
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("usersUploadDisplayPicture failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.UploadUserDisplayPictureRequest](../../models/operations/upload-user-display-picture-request.md)                                                                   | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[ReadableStream<Uint8Array>](../../models/.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## getDisplayPicture

Retrieve the current user's display picture image.<br><br>
<b>Overview:</b><br>
This endpoint returns the user's profile picture as binary image data. Use this for displaying the user's avatar in the application.<br><br>
<b>Response Format:</b><br>
<ul>
<li>Returns raw image data (not JSON)</li>
<li>Content-Type header indicates image format (typically image/jpeg)</li>
<li>Suitable for use directly in &lt;img&gt; src or CSS background</li>
</ul>
<b>Caching:</b><br>
<ul>
<li>Response includes cache headers for browser caching</li>
<li>Use ETag for conditional requests</li>
<li>Cache invalidated when picture is updated</li>
</ul>
<b>Alternative:</b><br>
For signed URL access, use the user profile endpoint which returns a <code>displayPictureUrl</code> field.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="getUserDisplayPicture" method="get" path="/users/dp" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.users.getDisplayPicture();

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { usersGetDisplayPicture } from "pipeshub/funcs/users-get-display-picture.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await usersGetDisplayPicture(pipeshub);
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("usersGetDisplayPicture failed:", res.error);
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

**Promise\<[operations.GetUserDisplayPictureResponse](../../models/operations/get-user-display-picture-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## removeDisplayPicture

Remove the current user's display picture and revert to default avatar.<br><br>
<b>Overview:</b><br>
This endpoint permanently removes the user's uploaded profile picture. After removal, the user will display a default avatar (typically initials or generic icon).<br><br>
<b>What Happens:</b><br>
<ul>
<li>Profile picture file is deleted from storage</li>
<li>User profile updated to remove picture reference</li>
<li>Cached images invalidated</li>
<li>Default avatar will be shown in UI</li>
</ul>
<b>Note:</b><br>
This action is immediate and irreversible. To restore a picture, user must upload a new one.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="removeUserDisplayPicture" method="delete" path="/users/dp" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.users.removeDisplayPicture();

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { usersRemoveDisplayPicture } from "pipeshub/funcs/users-remove-display-picture.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await usersRemoveDisplayPicture(pipeshub);
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("usersRemoveDisplayPicture failed:", res.error);
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

**Promise\<[operations.RemoveUserDisplayPictureResponse](../../models/operations/remove-user-display-picture-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## bulkInvite

Invite multiple users to the organization in a single operation. Ideal for onboarding entire teams at once.<br><br>
<b>Overview:</b><br>
This endpoint creates user accounts for multiple email addresses and sends invitation emails to all of them. It's the most efficient way to add multiple users to your organization.<br><br>
<b>Invitation Flow:</b><br>
<ol>
<li>Validate all email addresses</li>
<li>Check for existing accounts (skip duplicates)</li>
<li>Create user accounts for new emails</li>
<li>Restore any previously deleted accounts</li>
<li>Add users to specified groups (optional)</li>
<li>Send invitation emails to all new users</li>
</ol>
<b>Requirements:</b><br>
<ul>
<li><b>Account Type:</b> Business accounts only (not individual)</li>
<li><b>SMTP:</b> Email configuration must be set up</li>
<li><b>Authorization:</b> Admin privileges required</li>
</ul>
<b>Email Processing:</b><br>
<ul>
<li>Duplicate emails are automatically skipped</li>
<li>Invalid email formats are rejected</li>
<li>Existing users are not re-invited (use resend-invite)</li>
<li>Previously deleted users are restored</li>
</ul>
<b>Response Details:</b><br>
Response includes count of successful invites and any failures with reasons.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="bulkInviteUsers" method="post" path="/users/bulk/invite" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.users.bulkInvite({
    emails: [
      "user1@company.com",
      "user2@company.com",
    ],
    groupIds: [
      "507f1f77bcf86cd799439011",
    ],
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { usersBulkInvite } from "pipeshub/funcs/users-bulk-invite.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await usersBulkInvite(pipeshub, {
    emails: [
      "user1@company.com",
      "user2@company.com",
    ],
    groupIds: [
      "507f1f77bcf86cd799439011",
    ],
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("usersBulkInvite failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.BulkInviteUsersRequest](../../models/operations/bulk-invite-users-request.md)                                                                                      | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.BulkInviteUsersResponse](../../models/operations/bulk-invite-users-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## resendInvite

Resend the invitation email to a user who hasn't completed their account setup.<br><br>
<b>Overview:</b><br>
This endpoint resends the invitation email to a user who was previously invited but hasn't logged in yet. Useful when the original invitation email was lost, expired, or ended up in spam.<br><br>
<b>When to Use:</b><br>
<ul>
<li>User didn't receive original invitation</li>
<li>Invitation link expired</li>
<li>User forgot to complete setup</li>
<li>Email went to spam folder</li>
</ul>
<b>Requirements:</b><br>
<ul>
<li>User must exist in the system</li>
<li>User must NOT have logged in yet (hasLoggedIn: false)</li>
<li>SMTP configuration must be active</li>
<li>Admin privileges required</li>
</ul>
<b>What Happens:</b><br>
<ul>
<li>Generates a new invitation token</li>
<li>Invalidates any previous invitation links</li>
<li>Sends new invitation email</li>
<li>Resets invitation expiry timer</li>
</ul>


### Example Usage

<!-- UsageSnippet language="typescript" operationID="resendUserInvite" method="post" path="/users/{id}/resend-invite" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.users.resendInvite({
    id: "507f1f77bcf86cd799439011",
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { usersResendInvite } from "pipeshub/funcs/users-resend-invite.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await usersResendInvite(pipeshub, {
    id: "507f1f77bcf86cd799439011",
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("usersResendInvite failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.ResendUserInviteRequest](../../models/operations/resend-user-invite-request.md)                                                                                    | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.ResendUserInviteResponse](../../models/operations/resend-user-invite-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## listGraph

Retrieve a paginated list of users with enhanced search capabilities using the graph service.<br><br>
<b>Overview:</b><br>
This endpoint provides advanced user listing with full-text search, pagination, and optional relationship data from the knowledge graph. It's optimized for large organizations with thousands of users.<br><br>
<b>Search Capabilities:</b><br>
<ul>
<li>Full-text search across name and email</li>
<li>Fuzzy matching for typo tolerance</li>
<li>Results ranked by relevance</li>
</ul>
<b>Use Cases:</b><br>
<ul>
<li>User directory with search</li>
<li>Autocomplete user selection</li>
<li>Admin user management lists</li>
<li>User analytics dashboards</li>
</ul>
<b>Performance:</b><br>
<ul>
<li>Powered by graph database for fast queries</li>
<li>Supports pagination for large datasets</li>
<li>Results cached for repeated queries</li>
</ul>
<b>vs /users endpoint:</b><br>
Use this endpoint when you need advanced search or are dealing with large user bases. Use <code>/users</code> for simple full-list retrieval.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="listUsersGraph" method="get" path="/users/graph/list" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.users.listGraph({
    search: "john",
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { usersListGraph } from "pipeshub/funcs/users-list-graph.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await usersListGraph(pipeshub, {
    search: "john",
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("usersListGraph failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.ListUsersGraphRequest](../../models/operations/list-users-graph-request.md)                                                                                        | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.ListUsersGraphResponse](../../models/operations/list-users-graph-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## listTeams

Get teams that the current user belongs to

### Example Usage

<!-- UsageSnippet language="typescript" operationID="getCurrentUserTeams" method="get" path="/users/teams/list" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.users.listTeams();

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { usersListTeams } from "pipeshub/funcs/users-list-teams.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await usersListTeams(pipeshub);
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("usersListTeams failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.GetCurrentUserTeamsRequest](../../models/operations/get-current-user-teams-request.md)                                                                             | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[models.Team[]](../../models/.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |