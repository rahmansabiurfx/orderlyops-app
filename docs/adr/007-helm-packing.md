ADR-007: Helm Packaging Standard

    Status: Approved

    Context: We have multiple microservices like chat-api, embedding-worker moving through three different environments. Writing raw, static Kubernetes YAML files for each environment would mean duplicating thousands of lines of code, leading to massive configuration drift.

    Decision: Helm Charts (Internal Umbrella Pattern)

    Why Helm?

        Benefit: Write One time and then parameterize everywhere. Helm allows us to turn our Kubernetes manifests into templates. We define how the chat-api deploys once and then use a simple values.yaml file for each environment to swap out parameters like replica counts, ingress URLs and environment variables.

        Version Control for Configs: It treats our Kubernetes configurations like software packages. We can easily roll back a release if a specific configuration change breaks the staging environment.

    Consequences: Helm templates use Go templating syntax, which can quickly become a messy, unreadable puzzle of brackets ({{ ... }}) if over-engineered. We will keep our charts simple and avoid deep nesting to ensure the code remains maintainable.