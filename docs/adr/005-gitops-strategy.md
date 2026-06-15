ADR-005: GitOps Strategy

    Status: Approved

    Context:

    Decision: Declarative GitOps with a Dedicated GitOps Repository (orderlyops-app-gitops)

    Why this approach?

        Separation of Concerns: By keeping the application code (orderlyops-app) separate from the deployment manifests (orderlyops-app-gitops), a simple documentation or code fix won't accidentally trigger an entire cluster infrastructure sync.

        Git as the Source of Truth:

    Consequences: Any manual changes made directly to the cluster via the CLI will be automatically overwritten and reverted by the GitOps controller to match Git.