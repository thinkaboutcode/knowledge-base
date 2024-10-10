# Cloud Infrastructure as Code (IaC) Tools Cheatsheet

## Overview
This cheatsheet provides an overview of various frameworks and tools that enable you to define and manage cloud infrastructure using modern programming languages. These tools facilitate the infrastructure as code (IaC) paradigm, enhancing developer experience and operational efficiency.

---

| **Tool**               | **Supported Languages**          | **Key Features**                                           | **Use Cases**                                         | **Popularity**                     | **Website**                           |
|------------------------|----------------------------------|-----------------------------------------------------------|------------------------------------------------------|------------------------------------|---------------------------------------|
| **Pulumi**             | Python, JavaScript/TypeScript, Go, C#, Java | - Multi-cloud support<br>- Declarative & imperative<br>- State management | Cloud infrastructure, Kubernetes management, serverless applications | Growing; over 25k GitHub stars | [pulumi.com](https://www.pulumi.com/) |
| **CDK (Cloud Development Kit)** | TypeScript, Python, Java, .NET, Go | - Define cloud resources with familiar programming languages<br>- Higher-level abstractions for AWS services | AWS resource provisioning, serverless applications | Popular; 30k+ GitHub stars         | [aws.amazon.com/cdk](https://aws.amazon.com/cdk/) |
| **Terraform CDK (CDKTF)** | TypeScript, Python, Java, Go | - Use familiar programming languages with Terraform<br>- Supports Terraform modules and providers | Multi-cloud infrastructure management | Emerging; ~7k GitHub stars        | [cdk.tf](https://cdk.tf/) |
| **Ansible**            | YAML, Python                     | - Agentless<br>- Configuration management<br>- Infrastructure provisioning | Configuration management, application deployment | Very popular; ~58k GitHub stars   | [ansible.com](https://www.ansible.com/) |
| **Chef**               | Ruby                             | - Configuration management<br>- Infrastructure automation | Configuration management, infrastructure provisioning | Popular; ~28k GitHub stars         | [chef.io](https://www.chef.io/) |
| **SaltStack**          | Python                           | - Event-driven automation<br>- Configuration management<br>- Orchestration | System management, cloud provisioning | Moderate; ~13k GitHub stars        | [saltproject.io](https://saltproject.io/) |
| **Terraform**          | HCL (HashiCorp Configuration Language), JSON | - Declarative syntax<br>- Extensive provider ecosystem<br>- State management | Infrastructure provisioning across multiple clouds | Very popular; ~38k GitHub stars    | [hashicorp.com/terraform](https://www.hashicorp.com/products/terraform) |
| **Crossplane**         | Go                               | - Kubernetes-native<br>- Provisioning of cloud resources from within Kubernetes | Managing cloud resources via Kubernetes | Growing; ~8k GitHub stars          | [crossplane.io](https://crossplane.io/) |
| **Serverless Framework** | JavaScript, Python, Go, Java, .NET | - Simplifies serverless app deployment<br>- Multi-cloud support | Building serverless applications across multiple cloud providers | Very popular; ~43k GitHub stars   | [serverless.com](https://www.serverless.com/) |
| **Kubernetes Operators** | Go, Python, Java, etc.          | - Extends Kubernetes API<br>- Automates deployment and management | Application lifecycle management in Kubernetes | Growing; many implementations      | [kubernetes.io/docs/concepts/extend-kubernetes/operator](https://kubernetes.io/docs/concepts/extend-kubernetes/operator/) |
| **KubeVela**           | Go, YAML                         | - Application-centric<br>- Simplified deployment to Kubernetes | Deploying and managing applications on Kubernetes | Emerging; ~2k GitHub stars         | [kubevela.net](https://kubevela.net/) |
| **Jenkins X**          | Go, YAML                         | - CI/CD for Kubernetes<br>- GitOps integration           | Continuous delivery of applications on Kubernetes | Moderate; ~14k GitHub stars        | [jenkins-x.io](https://jenkins-x.io/) |
| **GitLab CI/CD**       | YAML                             | - Integrated CI/CD within GitLab<br>- Supports custom scripts and runners | Continuous integration and deployment pipelines | Very popular; widely adopted       | [gitlab.com](https://about.gitlab.com/stages-devops-lifecycle/continuous-integration/) |
| **OpenShift GitOps**   | YAML                             | - GitOps-based deployment<br>- Integrated with OpenShift   | GitOps workflows for Kubernetes applications         | Moderate; part of OpenShift ecosystem | [openshift.com](https://www.openshift.com/) |

---

## Key Considerations
- **Ease of Use**: Choose a tool that fits your team's skill set and existing workflows.
- **Multi-Cloud vs Single Cloud**: Some tools support multiple cloud providers, while others are tailored for specific platforms (e.g., AWS, Azure).
- **Integration with CI/CD**: Ensure the tool integrates well with your CI/CD pipeline.
- **Community and Support**: Consider the community support and documentation available for the tool.

---

## Conclusion
This cheatsheet provides a quick reference for various tools and frameworks available for defining cloud infrastructure using modern programming languages. Depending on your specific needs, team skills, and cloud strategy, one or more of these tools may be suitable for your projects.
