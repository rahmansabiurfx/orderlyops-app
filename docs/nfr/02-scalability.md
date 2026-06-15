The platform must scale to support 100+ concurrent users during peak traffic, but must automatically scale down to a near-zero cost when idle.

Architectural StrategyQueue-Based Ingestion: Asynchronous decoupling. High-overhead workloads (pipeline runs, Ragas evaluations) are immediately pushed to a message queue to buffer incoming spikes.

KEDA (Scale-to-Zero): Kubernetes Event-driven Autoscaling monitors the queue depth. When the queue is empty, KEDA scales worker pods down to 0 to eliminate idle compute costs. When a message arrives, it wakes the system up.

HPA (Scale-Out): Once active the Horizontal Pod Autoscaler handles real-time concurrency by duplicating pods based on CPU/Memory thresholds to process the queue in parallel.