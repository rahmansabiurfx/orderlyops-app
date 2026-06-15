# Sequence Diagram
# Document Ingestion

```mermaid
sequenceDiagram

actor Admin

participant API

participant S3

participant SQS

participant Worker

participant Embedder

participant Qdrant

Admin->>API: Upload Document

API->>S3: Store File

API->>SQS: Publish Event

SQS-->>Worker: Receive Message

Worker->>S3: Download Document

Worker->>Embedder: Chunk + Embed

Embedder-->>Worker: Embeddings

Worker->>Qdrant: Upsert Vectors

Worker->>SQS: Delete Message
```
