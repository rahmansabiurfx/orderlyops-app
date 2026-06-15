ADR-015: Standardized Observability

    Status: Approved.

    Context: We need to see how a query travels from the API to the LLM and back.

    Decision: OpenTelemetry (OTEL).

    Why: It is tech-agnostic. We can swap our backend from Grafana to something else later without rewriting a single line of instrumentation code.

    Consequences: Requires manual instrumentation in our Python code to get the best traces.