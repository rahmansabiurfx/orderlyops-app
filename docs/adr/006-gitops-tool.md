ADR-006: GitOps Tool

    Status: Approved

    Context: The GitOps strategy needs a Kubernetes controller that watches the Git repository and applies changes to the EKS cluster automatically. The two industry standards are ArgoCD and FluxCD.

    Decision: ArgoCD

    Why ArgoCD?

        The Visualization UI: ArgoCD comes with a visual web dashboard that maps out every single Kubernetes resource (pods, services, ingresses) and how they link together. It makes debugging deployment failures incredibly fast.

        Argo Ecosystem Synergy: Since we will be using Argo Rollouts for canary deployments and metric-based progressive delivery, sticking to the same ecosystem makes integration effortless.

        App-of-Apps Pattern: It natively handles complex multi-environment structures (dev, staging, prod) using a single master application configuration.

    Consequences: ArgoCD requires running a web UI and several custom controllers inside the cluster, which eats up more memory and CPU than Flux's ultra-lightweight, headless design. We accept this resource cost for the visibility it gives us.