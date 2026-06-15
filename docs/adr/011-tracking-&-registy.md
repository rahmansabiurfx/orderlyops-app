ADR-011: Tracking & Registry

    Status: Approved.

    Context: We need to track which prompts and models are winning and manage their lifecycle.

    Decision: MLflow.

    Why: It provides a unified dashboard for prompt versioning and a centralized Model Registry. It makes our project a professional, auditable pipeline.

    Consequences: Requires hosting and maintaining a tracking server and a backend SQL database.