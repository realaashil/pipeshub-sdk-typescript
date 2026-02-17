# OrganizationAuthConfigs

## Overview

### Available Operations

* [create](#create) - Create organization authentication configuration

## create

Create initial organization authentication configuration during onboarding.
This endpoint creates a new organization with admin user and default auth settings.
<br><br>
<b>Note:</b> This is typically called during the initial setup process.


### Example Usage

<!-- UsageSnippet language="typescript" operationID="createOrgAuthConfig" method="post" path="/orgAuthConfig/" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
});

async function run() {
  const result = await pipeshub.organizationAuthConfigs.create({
    contactEmail: "Tiana.Muller@hotmail.com",
    registeredName: "<value>",
    adminFullName: "<value>",
  });

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { organizationAuthConfigsCreate } from "pipeshub/funcs/organization-auth-configs-create.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
});

async function run() {
  const res = await organizationAuthConfigsCreate(pipeshub, {
    contactEmail: "Tiana.Muller@hotmail.com",
    registeredName: "<value>",
    adminFullName: "<value>",
  });
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("organizationAuthConfigsCreate failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [models.OrgAuthConfigCreateRequest](../../models/org-auth-config-create-request.md)                                                                                            | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<[operations.CreateOrgAuthConfigResponse](../../models/operations/create-org-auth-config-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.AuthError            | 400                         | application/json            |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |