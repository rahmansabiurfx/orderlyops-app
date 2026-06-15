ADR-001: Cloud Provider Selection

    Status: Approved

    Context: OrderlyOps needs a cloud foundation that can handle managed Kubernetes, event-driven queues, fast NoSQL storage and solid security boundaries. We need a provider with a massive ecosystem so we don't have to build core infrastructure components from scratch.

    Decision: Amazon Web Services (AWS)

    Tools: AWS has native services for everything our architecture requires (SQS for queuing, DynamoDB for session states, S3 for our data lake).

        Advanced Scaling: It natively supports Karpenter for cutting EKS cluster costs by smartly packing nodes.

        Identity Mapping: AWS has IRSA (IAM Roles for Service Accounts). This means EKS pods can talk to S3 or Secrets Manager using temporary, short-lived tokens instead of hardcoded API keys.

    Consequences: We are choosing AWS ecosystem, which means some cloud lock-in. However, since our core application and deployment logic live in Kubernetes and ArgoCD, the actual app migration to another cloud later wouldn't require a total rewrite.