ADR-004: VPC Network Architecture

    Status: Approved

    The Problem: OrderlyOps handles proprietary company data, but it still needs to talk to external LLM APIs like OpenAI and Groq to generate answers. We need a network setup that will keep our databases invisible to the public internet while allowing our app workers to make safe outbound API calls and will stays online even if an AWS data center crashes.

    The Decision: We are implementing a 3-Tier VPC Topology spread across 2 Availability Zones.

We are splitting the network into three distinct zones:

    Public Tier: Only houses our AWS Application Load Balancers (ALB) to accept user traffic.

    Private Tier: Houses the FastAPI app and Embedding Worker nodes. They cannot be reached directly from the internet but they can safely call external LLMs using a NAT Gateway.

    Isolated Tier: Completely isolated. This is where Qdrant (Vector DB), Redis and DynamoDB live. They have zero internet access—inbound or outbound—and can only talk to the EKS pods in private tier.

    Why this works: It provides isolation. Even if somehow the public load balancer is compromised, no one can access data layer. Spreading across 2 AZs guarantees high availability if an entire AWS facility goes dark.

    Consequences: Running NAT Gateways across 2 AZs gets expensive quickly because AWS charges a flat hourly rate for each one. To keep the cloud bill low a single NAT gateway will be used for dev and staging. The full multi-AZ NAT setup will be used in Production.