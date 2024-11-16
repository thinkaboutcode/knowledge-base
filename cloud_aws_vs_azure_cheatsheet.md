| **AWS Service**                          | **Azure Service**                           | **Description**                                                                 |
|------------------------------------------|---------------------------------------------|---------------------------------------------------------------------------------|
| **Compute**                              |                                             |                                                                                 |
| EC2 (Elastic Compute Cloud)              | Azure Virtual Machines                      | Scalable compute resources in the cloud.                                        |
| AWS Lambda                               | Azure Functions                             | Serverless compute for running code in response to events.                      |
| Elastic Beanstalk                        | Azure App Services                          | Managed platform for deploying and scaling web applications.                    |
| AWS Lightsail                            | Azure App Service Plans (or Virtual Machines)| Simplified cloud service for small-scale applications.                          |
| AWS Batch                                | Azure Batch                                 | Managed service for running batch computing workloads in containers.            |
| **Container Services**                   |                                             |                                                                                 |
| Amazon ECS (Elastic Container Service)   | Azure Kubernetes Service (AKS)              | Container orchestration and management service.                                |
| Amazon EKS (Elastic Kubernetes Service)  | Azure Kubernetes Service (AKS)              | Managed Kubernetes service for container orchestration.                         |
| AWS Fargate                              | Azure Container Instances                   | Serverless container management service.                                        |
| Amazon ECR (Elastic Container Registry)  | Azure Container Registry                    | Managed Docker container registry service.                                      |
| AWS App Runner                           | Azure App Service for Containers            | Managed service for running containerized applications at scale.                |
| **Storage**                              |                                             |                                                                                 |
| Amazon S3 (Simple Storage Service)       | Azure Blob Storage                          | Object storage for unstructured data.                                            |
| Amazon EBS (Elastic Block Store)         | Azure Managed Disks                         | Block storage for persistent data.                                               |
| Amazon EFS (Elastic File System)         | Azure Files                                 | Managed file shares for cloud applications.                                      |
| AWS Glacier                              | Azure Blob Storage (Cool / Archive tiers)   | Low-cost, long-term archive storage.                                             |
| **Networking**                           |                                             |                                                                                 |
| Amazon VPC (Virtual Private Cloud)       | Azure Virtual Network                       | Virtual private network for cloud resources.                                    |
| AWS Route 53                             | Azure DNS                                   | Domain Name System (DNS) service.                                                |
| AWS ELB (Elastic Load Balancer)          | Azure Load Balancer                         | Distributes traffic across multiple resources.                                  |
| AWS Direct Connect                       | Azure ExpressRoute                          | Dedicated, private network connection to the cloud.                             |
| **Content Delivery & CDN**               |                                             |                                                                                 |
| Amazon CloudFront                        | Azure Content Delivery Network (CDN)        | Content delivery and caching service for faster web delivery.                  |
| **Database**                             |                                             |                                                                                 |
| Amazon RDS (Relational Database Service) | Azure SQL Database                          | Managed relational database service.                                             |
| Amazon DynamoDB                          | Azure Cosmos DB                             | Managed NoSQL database service.                                                  |
| Amazon DocumentDB                        | Azure Cosmos DB (MongoDB API)               | Managed document database service for JSON-like data (MongoDB compatible).       |
| Amazon Neptune                           | Azure Cosmos DB (Gremlin API)               | Managed graph database service for handling connected data.                      |
| Amazon Aurora                            | Azure Database for MySQL/PostgreSQL          | Managed MySQL and PostgreSQL databases.                                          |
| Amazon Redshift                          | Azure Synapse Analytics                     | Managed data warehouse service for analytics.                                   |
| Amazon ElastiCache                       | Azure Cache for Redis                       | Managed Redis cache service.                                                    |
| Amazon Timestream                        | Azure Time Series Insights                  | Managed service for time series data and analytics.                             |
| Amazon Managed Blockchain                | Azure Blockchain Service                    | Managed service for creating and managing blockchain networks.                  |
| **Application Integration**              |                                             |                                                                                 |
| Amazon SQS (Simple Queue Service)        | Azure Queue Storage                         | Managed message queuing service.                                                |
| Amazon SNS (Simple Notification Service) | Azure Service Bus                           | Managed service for sending messages and notifications.                         |
| AWS Managed MQ                           | Azure Service Bus                           | Managed message broker service (ActiveMQ and RabbitMQ compatible).              |
| Amazon MSK (Managed Streaming for Kafka) | Azure Event Hubs                            | Managed service for Apache Kafka and event streaming.                           |
| Amazon EventBridge                       | Azure Event Grid                            | Event-driven computing service for event management and routing.                |
| AWS Step Functions                       | Azure Logic Apps                            | Orchestration service for automating workflows and tasks.                       |
| AWS API Gateway                          | Azure API Management                        | Managed service for creating, deploying, and managing APIs.                      |
| AWS AppSync                              | Azure API Management                        | Managed service for building and connecting APIs.                               |
| **Identity & Access Management (IAM)**   |                                             |                                                                                 |
| AWS IAM                                  | Azure Active Directory                      | Identity management and access control service.                                 |
| AWS Cognito                              | Azure Active Directory B2C                  | User authentication and access control for apps.                               |
| **Security & Compliance**                |                                             |                                                                                 |
| AWS WAF (Web Application Firewall)       | Azure Web Application Firewall              | Protects web apps from common threats.                                          |
| AWS Network Firewall                     | Azure Firewall                              | Managed, scalable firewall service for controlling network traffic.             |
| AWS Firewall Manager                     | Azure Firewall Manager                      | Centralized management service for managing and configuring firewalls.          |
| AWS Shield                               | Azure DDoS Protection                       | Managed DDoS protection services.                                               |
| AWS GuardDuty                            | Azure Security Center                       | Threat detection and monitoring service.                                        |
| AWS Inspector                            | Azure Security Center (Advanced Threat Protection) | Security vulnerability assessments for applications.                           |
| AWS Detective                            | Azure Sentinel                              | Security investigation service for detecting, analyzing, and responding to threats. |
| AWS Macie                                | Microsoft Purview                           | Data security service for identifying and protecting sensitive data.            |
| AWS Security Hub                         | Azure Defender                              | Unified security management offering threat protection across Azure resources. |
| **Monitoring & Management**              |                                             |                                                                                 |
| Amazon CloudWatch                        | Azure Monitor                               | Monitoring service for cloud resources and applications.                        |
| AWS Config                               | Azure Policy                                | Configuration management and compliance tracking service.                       |
| AWS CloudTrail                           | Azure Activity Log                          | Service for logging API calls and tracking user activity.                       |
| AWS X-Ray                                | Azure Application Insights                  | Service for tracing and analyzing application performance.                      |
| AWS Systems Manager                      | Azure Automation                            | Service for managing and automating resources.                                  |
| **Developer Tools**                      |                                             |                                                                                 |
| AWS CodeCommit                           | Azure Repos                                 | Managed source control service.                                                 |
| AWS CodeBuild                            | Azure Pipelines                             | Continuous integration and build automation.                                    |
| AWS CodeDeploy                           | Azure DevOps                                | Managed application deployment service.                                         |
| AWS CodePipeline                         | Azure Pipelines                             | Continuous delivery and pipeline orchestration.                                 |
| AWS CloudFormation                       | Azure Resource Manager (ARM)                | Infrastructure as Code (IaC) service for defining cloud resources declaratively. |
| **Analytics**                            |                                             |                                                                                 |
| Amazon Kinesis                           | Azure Stream Analytics                      | Real-time data streaming and analytics service.                                 |
| AWS Glue                                 | Azure Data Factory                          | Managed ETL (Extract, Transform, Load) service.                                  |
| AWS EMR (Elastic MapReduce)              | Azure HDInsight                             | Big data processing framework (Hadoop/Spark).                                   |
| Amazon QuickSight                        | Power BI                                   | Business Intelligence and data visualization tool.                              |
| **Machine Learning & AI**                |                                             |                                                                                 |
| Amazon SageMaker                         | Azure Machine Learning                      | Managed service for building and deploying machine learning models.             |
| AWS Rekognition                          | Azure Computer Vision                       | Image and video analysis using AI models.                                       |
| AWS Lex                                  | Azure Bot Services                          | Conversational AI for creating chatbots.                                        |
| **IoT (Internet of Things)**             |                                             |                                                                                 |
| AWS IoT Core                             | Azure IoT Hub                               | Managed service for IoT devices and data.                                       |
| **Virtual Desktops**                     |                                             |                                                                                 |
| Amazon WorkSpaces                        | Azure Virtual Desktop                       | Managed virtual desktop service.                                                |
| **Business Applications**                |                                             |                                                                                 |
| Amazon Chime                             | Microsoft Teams                             | Communication and collaboration platform.                                       |
| **Migration & Transfer**                 |                                             |                                                                                 |
| AWS Migration Hub                        | Azure Migrate                               | Service for managing and tracking cloud migrations.                             |
| AWS Database Migration Service           | Azure Database Migration Service            | Managed service for migrating databases to the cloud.                           |
| AWS Snowball                             | Azure Data Box                              | Physical data transfer service for large-scale data migrations.                 |
