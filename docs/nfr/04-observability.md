Metrics: We use Prometheus to track the big numbers—request rates, error counts and p95 latencies. If the system starts sweating (high CPU or memory) metrics will reflect that.

Logs: Every service sends structured logs to Loki. Because they're structured, we can filter through millions of lines easily to find the exact error message.

Traces: Traces (via OpenTelemetry and Tempo) let us follow a single query as it jumps from the API to Qdrant and out to the LLM. It's the only way to see if the lag is coming from our code or an external API.

SLOs: This project will set clear targets, which means that 99% of our RAG responses will stream back in under 3 seconds. If we dip below that, it's a signal to stop new features and fix the issue.