# StorageConfiguration

## Overview

### Available Operations

* [configureLocal](#configurelocal) - Configure Local Storage
* [createS3StorageConfig](#creates3storageconfig) - Configure AWS S3 Storage
* [createAzureBlob](#createazureblob) - Configure Azure Blob Storage
* [get](#get) - Get current storage configuration

## configureLocal

Configure local filesystem as the storage backend for file uploads and document storage. Suitable for development or on-premise deployments.

### Example Usage

<!-- UsageSnippet language="typescript" operationID="createLocalStorageConfig" method="post" path="/configurationManager/storageConfig#local" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  await pipeshub.storageConfiguration.configureLocal({
    storageType: "local",
    baseUrl: "http://localhost:3000/storage",
  });


}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { storageConfigurationConfigureLocal } from "pipeshub/funcs/storage-configuration-configure-local.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await storageConfigurationConfigureLocal(pipeshub, {
    storageType: "local",
    baseUrl: "http://localhost:3000/storage",
  });
  if (res.ok) {
    const { value: result } = res;
    
  } else {
    console.log("storageConfigurationConfigureLocal failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.CreateLocalStorageConfigRequest](../../models/operations/create-local-storage-config-request.md)                                                                   | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<void\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## createS3StorageConfig

Configure AWS S3 as the storage backend for file uploads and document storage. Requires an S3 bucket and IAM credentials with appropriate permissions.

### Example Usage

<!-- UsageSnippet language="typescript" operationID="createS3StorageConfig" method="post" path="/configurationManager/storageConfig#s3" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  await pipeshub.storageConfiguration.createS3StorageConfig({
    storageType: "s3",
    s3AccessKeyId: "AKIAIOSFODNN7EXAMPLE",
    s3SecretAccessKey: "wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY",
    s3Region: "us-east-1",
    s3BucketName: "my-pipeshub-bucket",
  });


}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { storageConfigurationCreateS3StorageConfig } from "pipeshub/funcs/storage-configuration-create-s3-storage-config.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await storageConfigurationCreateS3StorageConfig(pipeshub, {
    storageType: "s3",
    s3AccessKeyId: "AKIAIOSFODNN7EXAMPLE",
    s3SecretAccessKey: "wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY",
    s3Region: "us-east-1",
    s3BucketName: "my-pipeshub-bucket",
  });
  if (res.ok) {
    const { value: result } = res;
    
  } else {
    console.log("storageConfigurationCreateS3StorageConfig failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.CreateS3StorageConfigRequest](../../models/operations/create-s3-storage-config-request.md)                                                                         | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<void\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## createAzureBlob

Configure Azure Blob Storage as the storage backend. You can provide either:
- A full connection string (azureBlobConnectionString), OR
- Individual credentials (accountName, accountKey, endpointProtocol, endpointSuffix)


### Example Usage

<!-- UsageSnippet language="typescript" operationID="createAzureBlobStorageConfig" method="post" path="/configurationManager/storageConfig#azureBlob" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  await pipeshub.storageConfiguration.createAzureBlob({
    storageType: "azureBlob",
    containerName: "pipeshub-files",
    azureBlobConnectionString: "DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey;EndpointSuffix=core.windows.net",
    accountName: "mystorageaccount",
    accountKey: "base64encodedaccountkey==",
  });


}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { storageConfigurationCreateAzureBlob } from "pipeshub/funcs/storage-configuration-create-azure-blob.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await storageConfigurationCreateAzureBlob(pipeshub, {
    storageType: "azureBlob",
    containerName: "pipeshub-files",
    azureBlobConnectionString: "DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey;EndpointSuffix=core.windows.net",
    accountName: "mystorageaccount",
    accountKey: "base64encodedaccountkey==",
  });
  if (res.ok) {
    const { value: result } = res;
    
  } else {
    console.log("storageConfigurationCreateAzureBlob failed:", res.error);
  }
}

run();
```

### Parameters

| Parameter                                                                                                                                                                      | Type                                                                                                                                                                           | Required                                                                                                                                                                       | Description                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `request`                                                                                                                                                                      | [operations.CreateAzureBlobStorageConfigRequest](../../models/operations/create-azure-blob-storage-config-request.md)                                                          | :heavy_check_mark:                                                                                                                                                             | The request object to use for the request.                                                                                                                                     |
| `options`                                                                                                                                                                      | RequestOptions                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                             | Used to set various options for making HTTP requests.                                                                                                                          |
| `options.fetchOptions`                                                                                                                                                         | [RequestInit](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options)                                                                                        | :heavy_minus_sign:                                                                                                                                                             | Options that are passed to the underlying HTTP request. This can be used to inject extra headers for examples. All `Request` options, except `method` and `body`, are allowed. |
| `options.retries`                                                                                                                                                              | [RetryConfig](../../lib/utils/retryconfig.md)                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                             | Enables retrying HTTP requests under certain failure conditions.                                                                                                               |

### Response

**Promise\<void\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |

## get

Retrieve the current storage backend configuration. Returns the configuration for whichever storage type is currently active (Local, S3, or Azure Blob).

### Example Usage

<!-- UsageSnippet language="typescript" operationID="getStorageConfig" method="get" path="/configurationManager/storageConfig" -->
```typescript
import { Pipeshub } from "pipeshub";

const pipeshub = new Pipeshub({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const result = await pipeshub.storageConfiguration.get();

  console.log(result);
}

run();
```

### Standalone function

The standalone function version of this method:

```typescript
import { PipeshubCore } from "pipeshub/core.js";
import { storageConfigurationGet } from "pipeshub/funcs/storage-configuration-get.js";

// Use `PipeshubCore` for best tree-shaking performance.
// You can create one instance of it to use across an application.
const pipeshub = new PipeshubCore({
  serverURL: "https://api.example.com",
  bearerAuth: process.env["PIPESHUB_BEARER_AUTH"] ?? "",
});

async function run() {
  const res = await storageConfigurationGet(pipeshub);
  if (res.ok) {
    const { value: result } = res;
    console.log(result);
  } else {
    console.log("storageConfigurationGet failed:", res.error);
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

**Promise\<[operations.GetStorageConfigResponse](../../models/operations/get-storage-config-response.md)\>**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.PipeshubDefaultError | 4XX, 5XX                    | \*/\*                       |