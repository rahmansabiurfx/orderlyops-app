# Primary Use Cases

---

# UC-001 — Ask a Question

## Primary Actor

Authenticated User

## Goal

Receive a context-aware response generated using the knowledge base.

## Preconditions

* User is authenticated.
* Chat service is available.
* Knowledge base has been indexed.

## Main Flow

1. User submits a question.
2. API validates the request.
3. Session history is retrieved.
4. Relevant document chunks are retrieved.
5. Retrieved context is re-ranked.
6. Prompt is constructed.
7. LLM generates a streamed response.
8. Conversation is persisted.
9. Response is streamed back to the user.

## Postconditions

* Conversation stored.
* Metrics recorded.
* Logs generated.
* Trace completed.

---

# UC-002 — Upload Documents

## Primary Actor

Administrator

## Goal

Add new knowledge to the platform.

## Preconditions

* Administrator authenticated.

## Main Flow

1. Upload document.
2. Store document in S3.
3. Publish processing event.
4. Return upload acknowledgement.

## Postconditions

* Document awaiting embedding.

---

# UC-003 — Generate Embeddings

## Primary Actor

Embedding Worker

## Trigger

Document uploaded.

## Main Flow

1. Receive SQS message.
2. Download document.
3. Extract text.
4. Chunk document.
5. Generate embeddings.
6. Upsert vectors into Qdrant.
7. Delete queue message.

## Alternate Flow

Processing fails.

* Retry.
* Move to DLQ after retry threshold.

---

# UC-004 — Retrieve Knowledge

## Primary Actor

Retrieval Service

## Goal

Retrieve relevant context.

## Main Flow

1. Embed user query.
2. Execute hybrid search.
3. Merge search results.
4. Re-rank retrieved chunks.
5. Return context.

---

# UC-005 — Deploy New Version

## Primary Actor

Platform Engineer

## Main Flow

1. Push application changes.
2. CI builds container.
3. Image scanned.
4. Image pushed to registry.
5. GitOps repository updated.
6. ArgoCD synchronizes cluster.
7. Canary deployment begins.

---

# UC-006 — Progressive Rollout

## Primary Actor

Argo Rollouts

## Main Flow

1. Deploy new ReplicaSet.
2. Route small percentage of traffic.
3. Monitor health metrics.
4. Increase traffic gradually.
5. Promote deployment.

## Alternate Flow

Metrics fail threshold.

* Abort rollout.
* Restore previous ReplicaSet.

---

# UC-007 — Run Evaluation

## Primary Actor

Evaluation Pipeline

## Trigger

Deployment completed.

## Main Flow

1. Execute evaluation dataset.
2. Run RAGAS metrics.
3. Publish scores.
4. Store MLflow experiment.
5. Export Prometheus metrics.

---

# UC-008 — Collect Feedback

## Primary Actor

Authenticated User

## Goal

Provide feedback on generated responses.

## Main Flow

1. User submits positive or negative feedback.
2. Feedback stored.
3. Metrics updated.
4. Feedback associated with conversation.

---

# UC-009 — Recover Platform

## Primary Actor

Platform Engineer

## Trigger

Infrastructure failure.

## Main Flow

1. Provision infrastructure using Terraform.
2. Bootstrap cluster.
3. Restore secrets.
4. Synchronize workloads using ArgoCD.
5. Restore persistent data.
6. Validate application health.

---

# UC-010 — Scale Platform

## Primary Actor

Kubernetes Control Plane

## Trigger

Resource utilization exceeds thresholds.

## Main Flow

1. HPA scales API workloads.
2. KEDA monitors queue depth.
3. Karpenter provisions compute capacity.
4. Traffic redistributed.

## Postconditions

Platform returns to target performance while maintaining cost efficiency.
