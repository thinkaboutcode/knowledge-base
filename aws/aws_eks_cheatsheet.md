# Main Components of Amazon EKS

Amazon EKS (Elastic Kubernetes Service) is a fully managed service that makes it easy to run Kubernetes on AWS without needing to install and operate your own Kubernetes control plane. The key components of EKS are as follows:

## 1. Clusters
- An **EKS cluster** is the central control point for Kubernetes workloads, managing all the resources required to run your applications.
- The cluster includes the Kubernetes control plane, which is managed by AWS, and the worker nodes (EC2 instances or Fargate).
- Each cluster can contain multiple nodes and services, and AWS manages the infrastructure and availability of the control plane.

## 2. Nodes
- **Nodes** are the EC2 instances or AWS Fargate that run your application containers.
- Worker nodes are part of the EKS cluster and run the Kubernetes **kubelet** to manage containers on the node.
- Nodes can be manually provisioned EC2 instances, or managed automatically using **Amazon EKS Node Groups**.

## 3. Node Groups
- **Node Groups** are collections of EC2 instances that provide the compute capacity for running workloads in an EKS cluster.
- You can create managed node groups, where AWS handles the scaling and updates, or self-managed node groups where you have more control over the node configuration.

## 4. Kubernetes Control Plane
- The **Kubernetes control plane** manages the state of the cluster and the orchestration of containers.
- In EKS, the control plane is fully managed by AWS and includes:
    - **API server**: The entry point for all Kubernetes requests.
    - **Controller manager**: Responsible for managing controllers that handle the state of the cluster.
    - **Scheduler**: Decides which node should run a pod based on available resources.

## 5. Pods
- A **pod** is the smallest and simplest Kubernetes object that can hold one or more containers.
- Pods are the units that are deployed, scaled, and managed by Kubernetes, and they share the same networking namespace and storage.

## 6. Deployments
- A **deployment** is a higher-level Kubernetes object that manages the lifecycle of pods.
- Deployments ensure that the specified number of pod replicas are running and automatically handles updates, rollbacks, and scaling of applications.

## 7. Services
- A **Kubernetes service** is a logical abstraction that defines a set of pods and a policy by which to access them.
- Services expose applications running in pods to internal or external clients. Common types of services include:
    - **ClusterIP** (internal access only)
    - **LoadBalancer** (external access through an ELB)
    - **NodePort** (access through a specific port on nodes)

## 8. Ingress Controllers
- An **Ingress Controller** is a Kubernetes resource that manages external access to services in a cluster, typically HTTP/S traffic.
- Ingress controllers use **Ingress resources** to define routing rules that expose HTTP endpoints or paths to services running in the cluster.

## 9. ConfigMaps and Secrets
- **ConfigMaps** store configuration data in key-value pairs that can be consumed by applications in Kubernetes pods.
- **Secrets** store sensitive data, such as passwords or API tokens, and can be securely consumed by pods and containers.

## 10. IAM Roles for Service Accounts (IRSA)
- **IAM Roles for Service Accounts (IRSA)** allow you to associate an IAM role with a Kubernetes service account, which grants the pods running under that service account access to AWS services.
- This integration provides fine-grained permissions and is essential for securely accessing AWS resources from within Kubernetes.

## 11. EKS Fargate
- **EKS Fargate** is a serverless compute engine that allows you to run Kubernetes pods without managing the underlying EC2 instances.
- Fargate provisions and manages the compute resources for pods, letting you focus on application development and scaling.

## 12. EKS Add-ons
- **EKS Add-ons** are pre-configured, managed Kubernetes software packages that can be installed into an EKS cluster, such as logging and monitoring solutions (e.g., Amazon CloudWatch, AWS VPC CNI plugin).
- EKS Add-ons simplify the management of common Kubernetes tools and integrations.

## 13. Kubernetes API Server
- The **Kubernetes API Server** is the entry point for managing the cluster and communicating with Kubernetes resources.
- EKS provides a fully managed API server that abstracts the management and scaling, while you interact with the API using `kubectl` or other tools.

## 14. Amazon VPC CNI Plugin
- The **Amazon VPC CNI Plugin** allows Kubernetes pods to have native VPC networking and access to AWS services.
- This plugin enables pods to have their own IP addresses within a VPC, simplifying networking and service discovery within the cluster.

## 15. CloudWatch Logs & Monitoring
- EKS integrates with **CloudWatch** for logging, monitoring, and alerting.
- It enables you to collect logs from Kubernetes workloads, monitor metrics such as CPU and memory usage, and set up alarms for specific conditions.
- **CloudWatch Container Insights** provides detailed metrics for containerized applications running in EKS.

These components work together to provide a fully managed, scalable, and highly available Kubernetes service, allowing you to focus on developing and deploying applications while AWS handles the underlying infrastructure management.
