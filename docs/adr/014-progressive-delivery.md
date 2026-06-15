ADR-014: Progressive Delivery

    Status: Approved.

    Context: A bad model deployment shouldn't take down the whole platform.

    Decision: Argo Rollouts.

    Why: It allows for Canary deployments. We can send 10% of traffic to a new model and automatically roll it back if Prometheus shows an error spike.

    Consequences: Adds a bit of complexity to our GitOps manifests.