# DownloadDocumentResponse


## Supported Types

### `operations.DownloadDocumentResponseBody`

```typescript
const value: operations.DownloadDocumentResponseBody = {
  success: true,
  signedUrl:
    "https://bucket.s3.amazonaws.com/docs/file.pdf?X-Amz-Signature=...",
};
```

### `ReadableStream<Uint8Array>`

```typescript
const value: ReadableStream<Uint8Array> = await openAsBlob("example.file");
```

