# What is GitOps?

GitOps is an operational framework that takes DevOps best practices used for application development such as version control, collaboration, compliance, and CI/CD, and applies them to infrastructure automation.

GitOps is not a single product, plugin, or platform. GitOps is an approach that leverages Git as a single source of truth for the desired state of the entire system, enabling continuous deployment of cloud-native applications. It works by using Git repositories as the source of truth for both application and infrastructure code, ensuring that any changes to the system are version-controlled, auditable, and can be rolled back.


GitOps requires three core components:

1. IaC : GitOps uses a Git repository as the single source of truth for infrastructure definitions. Git is an open source version control system that tracks code management changes, and a Git repository is a .git folder in a project that tracks all changes made to files in a project over time. Infrastructure as code (IaC) is the practice of keeping all infrastructure configuration stored as code. The actual desired state may or may not be not stored as code (e.g., number of replicas or pods).

2. MRs: GitOps uses merge requests (MRs) or pull requests (PRs) as the change mechanism for all infrastructure updates. The MR or PR is where teams can collaborate via reviews and comments and where formal approvals take place. A merge commits to your main (or trunk) branch and serves as an audit log or audit trail.

3. CI/CD: GitOps automates infrastructure updates using a Git workflow with continuous integration and continuous delivery (CI/CD). When new code is merged, the CI/CD pipeline enacts the change in the environment. Any configuration drift, such as manual changes or errors, is overwritten by GitOps automation so the environment converges on the desired state defined in Git. GitLab uses CI/CD pipelines to manage and implement GitOps automation, but other forms of automation, such as definitions operators, can be used as well.


There are two ways to implement the deployment strategy for GitOps: Push-based and Pull-based deployments. 

* Push-based Deployments:
The Push-based deployment strategy is implemented by popular CI/CD tools such as Jenkins, CircleCI, or Travis CI. The source code of the application lives inside the application repository along with the Kubernetes YAMLs needed to deploy the app. Whenever the application code is updated, the build pipeline is triggered, which builds the container images and finally the environment configuration repository is updated with new deployment descriptors. Changes to the environment configuration repository trigger the deployment pipeline.


* Pull-based Deployments:
Pull-based deployment approach, the operator is introduced. here you have a agent installed in the enviroment like in kubernetes cluster it takes over the role of the pipeline by actively pulling the changes from git repository, comparing the desired state in the environment repository with the actual state in the deployed infrastructure. Whenever differences are noticed, the operator updates the infrastructure to match the environment repository. Additionally the image registry can be monitored to find new versions of images to deploy.


https://volkswagengroup.sharepoint.com/sites/VWITSJAVAFullStackAWSCloudAoE/Shared%20Documents/Forms/AllItems.aspx
