# CreateLocalStorageConfigRequest

Request body for Configure Local Storage

## Example Usage

```typescript
import { CreateLocalStorageConfigRequest } from "pipeshub/models/operations";

let value: CreateLocalStorageConfigRequest = {
  storageType: "local",
  baseUrl: "http://localhost:3000/storage",
};
```

## Fields

| Field                                                                                                                 | Type                                                                                                                  | Required                                                                                                              | Description                                                                                                           | Example                                                                                                               |
| --------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| `storageType`                                                                                                         | [operations.CreateLocalStorageConfigStorageType](../../models/operations/create-local-storage-config-storage-type.md) | :heavy_check_mark:                                                                                                    | Storage type identifier                                                                                               | local                                                                                                                 |
| `mountName`                                                                                                           | *string*                                                                                                              | :heavy_minus_sign:                                                                                                    | Mount point name for local storage directory                                                                          | PipesHub                                                                                                              |
| `baseUrl`                                                                                                             | *string*                                                                                                              | :heavy_minus_sign:                                                                                                    | Base URL for accessing locally stored files                                                                           | http://localhost:3000/storage                                                                                         |