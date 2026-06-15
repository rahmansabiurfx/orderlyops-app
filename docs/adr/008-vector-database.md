ADR-008: Vector Database

    Status: Approved.

    Context: We need a vector store that can handle high-dimensional embeddings and complex metadata filtering for our knowledge base.

    Decision: Qdrant.

    Why: It supports Hybrid Search (BM25 + Vector) natively. This means we don't have to glue two different databases together to get both keyword and semantic accuracy.

    Consequences: We need to manage memory limits in Kubernetes, as vector indices live in RAM for speed.