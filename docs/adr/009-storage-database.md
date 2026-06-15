ADR-009: Long-term Storage Database

    Status: Approved.

    Context: We need a permanent, low-maintenance storage for conversation logs and audit trails.

    Decision: Amazon DynamoDB.

    Why: It's serverless and scales to zero. Since we don't need complex relational queries for logs, its high availability and speed make it perfect for archival.

    Consequences: We lose SQL-style querying; we have to be very intentional about our Partition Key design for future lookups.