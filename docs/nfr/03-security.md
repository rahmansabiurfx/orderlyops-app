The platform must eliminate hardcoded, long-lived, or static credentials. All system components must utilize runtime-injected, ephemeral secrets and least-privilege identity models, accompanied by automated container vulnerability mitigation.

IRSA (IAM Roles for Service Accounts): Eliminates static AWS access keys inside Kubernetes. Pods are mapped directly to AWS IAM roles using native Kubernetes Service Accounts. OpenID Connect (OIDC) authenticates the pod, granting temporary, short-lived AWS permissions dynamically.

AWS Secrets Manager: Centralized repository for third-party sensitive data (OpenAI API keys, database passwords etc.). Secrets are fetched programmatically at runtime via API or injected as ephemeral environment variables into the pods, completely removing credentials from Git.

Image Scanning (DevSecOps): Automated vulnerability tracking within the CI/CD pipeline and container registry . Every container image is scanned for CVEs (Common Vulnerabilities and Exposures) upon push. Deployments are blocked if "High" or "Critical" vulnerabilities are detected.

## Metrics & Verification
Credential Age: static long-lived AWS keys permitted in the codebase or cluster.
Vulnerability Threshold: Zero "Critical" or "High" CVEs allowed in production container images.
Testing: Verified via automated static analysis during Git pushes to catch accidental secret leaks, alongside automated pipeline step audits for container security compliance.