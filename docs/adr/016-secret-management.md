ADR-016: Secrets Management

    Status: Approved.

    Context: Hardcoded API keys in a repo are a security nightmare.

    Decision: AWS Secrets Manager + External Secrets Operator (ESO).

    Why: We store keys in a vault and ESO automatically syncs them into Kubernetes secrets. No static keys ever touch our Git repo.

    Consequences: We are dependent on the ESO operator; if it crashes, secrets might not rotate correctly.