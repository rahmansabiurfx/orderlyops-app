We will use three repositories for this project. One will contain infrastructure code, one will contain the apllication and the last one will be for gitops.

orderlyops-infra: We want infrastructure to stay separate from our application. So any changes to infra code will not run the whole pipeline.

orderlyops-app: Our RAG application will live here along with all the project documentations.

orderlyops-app-gitops: GitOps repo for the platform. Will contain the helm charts.