ADR-012: Data Versioning

    Status: Approved.

    Context: Large PDF corpuses and vector indices are way too big for Git.

    Decision: DVC (Data Version Control).

    Why: It lets us version our data exactly like we version our code, using S3 as the actual storage locker.

    Consequences: Developers have a slightly different workflow (dvc pull then git pull).