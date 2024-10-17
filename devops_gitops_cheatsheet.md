# GitOps Cheatsheet

## What is GitOps?
GitOps is a set of practices to manage infrastructure and application deployments using **Git** as the single source of truth. It automates the synchronization of your infrastructure and application state to match what is declared in Git.

### Key Concepts:
- **Git as Source of Truth**: All configurations (infrastructure, Kubernetes manifests, etc.) are stored in Git.
- **Declarative Infrastructure**: Infrastructure is defined using declarative configurations (e.g., YAML files for Kubernetes).
- **Automatic Syncing**: Tools like **Argo CD** or **Flux** automatically apply changes from Git to your Kubernetes cluster.
- **Pull-Based Model**: Instead of pushing changes, GitOps tools **pull** changes from Git and apply them to the cluster.
- **Continuous Monitoring**: The actual state of the system is continuously compared to the desired state in Git.
- **Version Control & Auditing**: Every change is tracked in Git, allowing for easy rollbacks and history tracking.

---

## GitOps Workflow:
1. **Commit to Git**: Changes to infrastructure or application configurations are committed to a Git repository.
2. **Pull Request**: A pull request (PR) is created for review and approval.
3. **Merge**: Once approved, changes are merged into the main branch.
4. **Automatic Sync**: GitOps tools like Argo CD or Flux automatically sync the desired state to the Kubernetes cluster.
5. **Monitoring**: GitOps tools monitor for any drift between the desired state (in Git) and the actual state (in the cluster).

---

## Tools for GitOps:
- **Argo CD**: A Kubernetes-native tool for deploying applications and managing Kubernetes clusters using GitOps principles.
- **Flux**: A GitOps tool to automate deployments to Kubernetes based on changes in Git.
- **Weave GitOps**: A fully integrated GitOps platform with UI and workflow automation.
- **Rancher Fleet**: A GitOps tool for managing multiple Kubernetes clusters.

---

## GitOps vs CI/CD Pipelines: Comparison Table

| **Aspect**                | **GitOps**                                                                                             | **CI/CD Pipelines**                                                                                     |
|---------------------------|--------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------|
| **Focus**                 | Infrastructure and Kubernetes application management using Git as the source of truth.                 | Automating build, testing, and deployment of application code.                                           |
| **Deployment Model**      | **Pull-based**: Kubernetes clusters pull changes from Git.                                              | **Push-based**: CI/CD pipelines push changes to the environment.                                         |
| **State Management**      | Declarative: Infrastructure and application state is declared in Git, and the actual state is synced.   | Imperative: Code changes are pushed through a series of steps to achieve the final state.                |
| **Version Control**       | GitOps uses Git for version control of infrastructure and application configurations.                   | CI/CD pipelines typically track application code versions, but may not always track infrastructure.       |
| **Automation Scope**      | Primarily for managing infrastructure and Kubernetes cluster configurations.                           | Automates the build, test, and deploy process for application code.                                      |
| **Tools**                 | **Flux**, **Argo CD**, **Weave GitOps**, **Rancher Fleet**.                                             | **Jenkins**, **CircleCI**, **GitLab CI**, **GitHub Actions**, **Travis CI**, **Tekton**, **Spinnaker**.   |
| **Environment Sync**      | Continuously monitors Git for changes and syncs the environment to the desired state.                   | Pushes changes to environments after running tests and validations in CI pipelines.                      |
| **Rollback Mechanism**    | Easy rollback by reverting commits in Git.                                                             | Rollbacks typically require redeploying a previous version of the application via a CI/CD pipeline.      |
| **Kubernetes Focus**      | GitOps is designed specifically for Kubernetes and cloud-native environments.                          | CI/CD pipelines can be used for any type of application, not necessarily Kubernetes-specific.            |
| **Drift Detection**       | Continuous drift detection: GitOps tools ensure the actual state matches the desired state in Git.      | CI/CD doesn’t natively monitor drift between the deployed state and the desired state.                   |

---

## Benefits of GitOps:
- **Improved Traceability**: Every change is tracked in Git, providing an auditable history.
- **Declarative Approach**: Infrastructure and application states are declared in YAML/Helm charts, ensuring consistent deployments.
- **Automated Rollbacks**: Easily revert to a previous state by reverting Git commits.
- **Continuous Reconciliation**: GitOps tools continuously check if the actual state matches the desired state defined in Git and reconcile if needed.
- **Scalability**: Suitable for managing multi-cluster and multi-environment Kubernetes deployments.

---

## Popular GitOps Tools
- **Argo CD**: Best for continuous delivery with GitOps in Kubernetes.
- **Flux**: Lightweight and simple GitOps tool for automated Kubernetes deployments.
- **Jenkins X**: Combines GitOps with CI/CD for cloud-native apps on Kubernetes.
- **Rancher Fleet**: GitOps-based management for large-scale Kubernetes clusters.

---

## How GitOps and CI/CD Complement Each Other:
1. **CI/CD for Code Changes**: CI/CD pipelines handle building and testing the application code.
2. **GitOps for Infrastructure & Deployments**: Once the CI pipeline passes, GitOps tools apply the new changes (e.g., Kubernetes manifests) from Git to the cluster.
3. **Combined Workflow**: CI/CD automates code building and testing, while GitOps ensures that infrastructure is always in sync with what’s defined in Git, ensuring safer, more reliable deployments.

---

## Example Workflow Combining CI/CD and GitOps:
1. **Developer commits code** to Git (e.g., feature branch).
2. **CI pipeline builds the code**, runs tests, and packages it (e.g., Docker image).
3. CI pipeline **updates Kubernetes manifests** with the new image version and commits the changes to the Git repository.
4. GitOps tool (e.g., Argo CD or Flux) **automatically syncs the Kubernetes cluster** with the new manifests, deploying the new version.
5. GitOps tool **monitors the cluster** to ensure it matches the desired state in Git.

---

