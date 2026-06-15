ADR-013: Model Evaluation

    Status: Approved.

    Context: We need to prove the bot isn't hallucinating before we deploy it.

    Decision: Ragas.

    Why: It provides automated "AI-as-a-judge" metrics like Faithfulness and Relevance. This lets us set hard quality gates in our CI/CD pipeline.

    Consequences: Running these tests costs LLM tokens; we have to budget for testing costs.