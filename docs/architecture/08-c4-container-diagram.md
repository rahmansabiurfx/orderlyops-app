# C4 Model - Level 2
# Container Diagram

## Purpose

This diagram illustrates the major containers (applications, databases, external systems) that make up the OrderlyOps platform and the relationships between them.

```mermaid


flowchart LR

subgraph Users
    User[End User]
    Admin[Administrator]
end

subgraph AWS

subgraph EKS Cluster

Ingress[NGINX Ingress]

ChatAPI[FastAPI Chat API]

Worker[Embedding Worker]

MLflow[MLflow]

Prefect[Prefect]

ArgoCD[ArgoCD]

Redis[(Redis)]

Qdrant[(Qdrant)]

end

Dynamo[(DynamoDB)]

S3[(S3)]

SQS[(SQS)]

Secrets[Secrets Manager]

end

Groq[LLM Provider]

Prometheus[Prometheus]

Grafana[Grafana]

Loki[Loki]

Tempo[Tempo]

User --> Ingress

Admin --> ArgoCD

Ingress --> ChatAPI

ChatAPI --> Redis

ChatAPI --> Qdrant

ChatAPI --> Dynamo

ChatAPI --> Groq

ChatAPI --> Prometheus

ChatAPI --> Loki

ChatAPI --> Tempo

S3 --> SQS

SQS --> Worker

Worker --> Qdrant

Worker --> S3

Worker --> Prometheus

MLflow --> S3

Prefect --> Worker

Prefect --> MLflow

ArgoCD --> ChatAPI

ArgoCD --> Worker

Prometheus --> Grafana

Loki --> Grafana

Tempo --> Grafana

Secrets --> ChatAPI

Secrets --> Worker

Secrets --> MLflow
```