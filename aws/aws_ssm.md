# Resources Managed by AWS Systems Manager (SSM)

## 1. Amazon EC2 Instances
- **Primary Use**: Manage configuration, patching, and automation for Amazon EC2 instances.
- **Capabilities**:
    - Patch management with **Patch Manager**.
    - Configuration management with **Run Command** and **State Manager**.
    - Monitoring compliance with **Compliance Manager**.
    - Automated workflows with **Automation Documents (SSM Documents)**.
    - Session-based remote management with **Session Manager**.

---

## 2. On-Premises Servers and Virtual Machines (Hybrid Resources)
- **Primary Use**: Extend SSM management capabilities to non-AWS environments.
- **Capabilities**:
    - Register on-premises servers or VMs as **managed instances** using the SSM Agent.
    - Perform patching, updates, and configuration using the same tools as EC2 instances.

---

## 3. AWS Elastic Kubernetes Service (EKS)
- **Primary Use**: Manage containerized workloads running on EKS.
- **Capabilities**:
    - Patch Kubernetes nodes using **Patch Manager**.
    - Execute commands on worker nodes with **Run Command**.
    - Automate workflows for Kubernetes clusters using **Automation Documents**.

---

## 4. Amazon ECS Container Instances
- **Primary Use**: Manage containerized workloads running on ECS (EC2 launch type).
- **Capabilities**:
    - Patch the underlying EC2 instances.
    - Execute automation workflows targeting ECS container instances.
    - Use **Session Manager** for remote access to the underlying EC2 instances.

---

## 5. AWS Systems Manager Application Manager
- **Primary Use**: Manage applications and related resources across AWS.
- **Capabilities**:
    - Group and manage application components (e.g., EC2 instances, databases, S3 buckets) using application tags.
    - Monitor application health and compliance.

---

## 6. Amazon RDS Instances
- **Primary Use**: Automate management tasks for relational databases.
- **Capabilities**:
    - Automate database maintenance tasks like backups or instance configurations using **Automation Documents**.
    - Integrate with **OpsCenter** for operational insights and issue resolution.

---

## 7. AWS Lambda Functions
- **Primary Use**: Trigger automation workflows and manage serverless resources.
- **Capabilities**:
    - Use Systems Manager **Automation Documents** to invoke Lambda functions.
    - Orchestrate workflows that include both managed instances and Lambda-based tasks.

---

## 8. Amazon S3
- **Primary Use**: Automate workflows involving S3 buckets and objects.
- **Capabilities**:
    - Use Automation Documents to manage bucket policies, replication, or lifecycle configurations.
    - Trigger custom workflows using S3 event integrations.

---

## 9. AWS CloudFormation Stacks
- **Primary Use**: Automate and manage CloudFormation resources.
- **Capabilities**:
    - Execute SSM Automation workflows on CloudFormation stacks.
    - Automate the creation, update, or deletion of stacks.

---

## 10. AWS Elastic Load Balancers (ELB)
- **Primary Use**: Automate ELB configurations and related workflows.
- **Capabilities**:
    - Automate certificate renewal or listener reconfiguration using Automation Documents.
    - Manage load balancer scaling and updates.

---

## 11. AWS Auto Scaling Groups
- **Primary Use**: Manage and automate Auto Scaling Group tasks.
- **Capabilities**:
    - Automate instance refresh for rolling updates to AMIs.
    - Automate configuration changes in Auto Scaling Groups.

---

## 12. Amazon CloudWatch Resources
- **Primary Use**: Enhance monitoring and automation of CloudWatch metrics and alarms.
- **Capabilities**:
    - Trigger SSM workflows based on CloudWatch alarms.
    - Use **Run Command** to respond to monitoring events.

---

## 13. Other AWS Resources
- **Amazon Route 53**: Automate DNS record management using Automation workflows.
- **AWS Directory Service**: Manage directory-related tasks.
- **Amazon DynamoDB**: Use workflows to automate table management tasks.

---

## 14. Taggable Resources
- **Primary Use**: Use tags to group and manage AWS resources.
- **Capabilities**:
    - Target operations using tags (e.g., EC2 instances, RDS databases, S3 buckets).
    - Manage resources at scale without specifying individual resource IDs.

---

## 15. Custom Resources
- **Primary Use**: Extend SSM capabilities to any resource using Automation workflows and Lambda functions.
- **Capabilities**:
    - Use custom Automation Documents to manage third-party applications or other AWS resources.

---

# Summary
AWS Systems Manager (SSM) is a versatile tool designed to manage a variety of AWS resources, including:
- EC2 instances
- On-premises servers (hybrid environments)
- EKS and ECS
- RDS databases
- S3 buckets
- Lambda functions

It integrates with tagging, automation, and patch management to streamline infrastructure and application management tasks.
