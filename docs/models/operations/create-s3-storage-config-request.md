# CreateS3StorageConfigRequest

Request body for Configure AWS S3 Storage

## Example Usage

```typescript
import { CreateS3StorageConfigRequest } from "pipeshub/models/operations";

let value: CreateS3StorageConfigRequest = {
  storageType: "s3",
  s3AccessKeyId: "AKIAIOSFODNN7EXAMPLE",
  s3SecretAccessKey: "wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY",
  s3Region: "us-east-1",
  s3BucketName: "my-pipeshub-bucket",
};
```

## Fields

| Field                                                                                                           | Type                                                                                                            | Required                                                                                                        | Description                                                                                                     | Example                                                                                                         |
| --------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| `storageType`                                                                                                   | [operations.CreateS3StorageConfigStorageType](../../models/operations/create-s3-storage-config-storage-type.md) | :heavy_check_mark:                                                                                              | Storage type identifier                                                                                         | s3                                                                                                              |
| `s3AccessKeyId`                                                                                                 | *string*                                                                                                        | :heavy_check_mark:                                                                                              | AWS IAM access key ID with S3 permissions                                                                       | AKIAIOSFODNN7EXAMPLE                                                                                            |
| `s3SecretAccessKey`                                                                                             | *string*                                                                                                        | :heavy_check_mark:                                                                                              | AWS IAM secret access key                                                                                       | wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY                                                                        |
| `s3Region`                                                                                                      | *string*                                                                                                        | :heavy_check_mark:                                                                                              | AWS region where the S3 bucket is located                                                                       | us-east-1                                                                                                       |
| `s3BucketName`                                                                                                  | *string*                                                                                                        | :heavy_check_mark:                                                                                              | Name of the S3 bucket for storing files                                                                         | my-pipeshub-bucket                                                                                              |