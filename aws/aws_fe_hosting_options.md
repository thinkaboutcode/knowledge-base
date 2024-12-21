# Frontend Hosting Architectures with AWS WAF

## 1. CloudFront and S3 for Static Frontends

**Architecture Flow**:
- User → AWS WAF → CloudFront → S3 (Frontend assets)

**Explanation**:
- In this setup, your frontend assets (HTML, CSS, JavaScript, images) are stored in an **S3** bucket, which serves as the origin.
- **CloudFront** is used as the Content Delivery Network (CDN) to cache and distribute the content globally to users.
- **AWS WAF** is applied at the **CloudFront** layer to filter incoming traffic and block threats like SQL injection and cross-site scripting (XSS).

**Benefits**:
- **Cost-effective**: Ideal for static websites or single-page applications (SPA).
- **Scalable**: **S3** scales automatically with traffic, and **CloudFront** ensures fast content delivery from edge locations globally.
- **Security**: **AWS WAF** protects against common threats such as SQL injection, cross-site scripting, and DDoS attacks.

**Limitations**:
- **Static Only**: Not suitable for dynamic content, server-side rendering (SSR), or complex business logic.
- **Limited custom logic**: You can’t handle dynamic requests or SSR directly in this setup.

---

## 2. CloudFront with Application Load Balancer (ALB) for Dynamic Frontends

**Architecture Flow**:
- User → AWS WAF → CloudFront → ALB → EC2/ECS/Fargate (Backend or dynamic frontend)

**Explanation**:
- In this architecture, **CloudFront** delivers cached or dynamically generated content based on requests.
- **AWS WAF** filters traffic at the **CloudFront** layer.
- Requests for dynamic content or SSR pages are forwarded by **CloudFront** to the **Application Load Balancer (ALB)**.
- **ALB** then routes the request to **EC2 instances**, **ECS containers**, or **Fargate**, where the frontend application logic is executed.

**Benefits**:
- **Scalable**: Supports both static and dynamic content (including SSR). The backend can scale automatically based on demand.
- **Global Distribution**: **CloudFront** provides caching and global delivery of static assets, and dynamic content is efficiently routed via **ALB**.
- **Security**: **AWS WAF** protects both **CloudFront** and **ALB** from malicious traffic.

**Limitations**:
- **Higher complexity**: Requires proper setup and management of **ALB**, **ECS/Fargate**, and backend services, making it more complex to configure.
- **Higher cost**: This setup involves more components and higher costs compared to simpler static hosting solutions like **S3** + **CloudFront**.

---

## 3. API Gateway as a Unified Access Point

**Architecture Flow**:
- User → AWS WAF → CloudFront → API Gateway → Lambda/ECS/EC2 (Backend services)

**Explanation**:
- This setup centralizes the access point to both the frontend and backend via **API Gateway**.
- **AWS WAF** protects **CloudFront**, and **CloudFront** can optionally cache static assets.
- **API Gateway** acts as a central hub, handling requests from the frontend and routing them to backend services like **Lambda**, **ECS**, or **EC2**.
- This is ideal for applications that have a combination of static and dynamic content and need robust API management features.

**Benefits**:
- **Centralized Access**: All traffic to the frontend and backend passes through a single entry point via **API Gateway**, which simplifies management.
- **Scalable**: **API Gateway** and **Lambda** scale automatically with traffic, ensuring your application can handle increased loads.
- **Security**: **AWS WAF** provides comprehensive protection for both the **API Gateway** and backend services.
- **Flexible**: Can integrate with serverless (**Lambda**) or containerized (**ECS**) backend services.

**Limitations**:
- **Slight latency**: There is a small amount of added latency because of the processing done by **API Gateway**.
- **Cost**: Depending on the volume of requests, **API Gateway** can become expensive at high traffic levels.

---

## 4. CloudFront and S3 with Lambda@Edge for Custom Logic

**Architecture Flow**:
- User → AWS WAF → CloudFront → Lambda@Edge → S3 (Frontend assets)

**Explanation**:
- **S3** stores the static assets, and **CloudFront** serves them to users globally.
- **AWS WAF** protects traffic at the **CloudFront** layer.
- **Lambda@Edge** runs custom logic at CloudFront edge locations, such as modifying headers, performing redirects, or adding authentication.
- After the custom logic is applied, the frontend assets are fetched from **S3**.

**Benefits**:
- **Low-latency logic**: **Lambda@Edge** enables you to execute dynamic behavior such as header manipulation or URL redirects at the edge locations, reducing latency.
- **Cost-effective**: The approach is ideal for injecting small amounts of custom logic without the need for a full backend server.
- **Global Distribution**: With **CloudFront** and **Lambda@Edge**, the custom logic is applied as close to the user as possible.
- **Security**: **AWS WAF** provides protection for all incoming requests.

**Limitations**:
- **Limited compute**: **Lambda@Edge** has strict limitations on execution time and resources (50ms max execution time per invocation).
- **Not for complex SSR**: Not suitable for complex dynamic logic or server-side rendering; it's better for lightweight tasks like URL rewriting or request validation.

---

## 5. CloudFront with AWS App Runner

**Architecture Flow**:
- User → AWS WAF → CloudFront → AWS App Runner (Containerized frontend)

**Explanation**:
- **AWS App Runner** is used to run containerized applications, such as React or Angular apps, in a fully managed environment.
- **CloudFront** acts as the CDN to serve the content globally, while **AWS WAF** secures traffic before it reaches **App Runner**.
- **App Runner** automatically handles scaling and traffic distribution based on demand.

**Benefits**:
- **Fully managed**: **App Runner** abstracts away the infrastructure management for containerized applications, reducing operational overhead.
- **Scalable**: It automatically scales based on traffic and only charges for the resources used.
- **Security**: **AWS WAF** protects your application from malicious traffic.
- **Easy setup**: **App Runner** simplifies deployment, and it's integrated with **AWS CodePipeline** for CI/CD workflows.

**Limitations**:
- **Limited customization**: **App Runner** may not offer the same level of flexibility as **ECS** or **EC2** for more complex application requirements.
- **Higher cost**: Compared to simpler static hosting solutions (like **S3** + **CloudFront**), it may incur higher costs due to the managed environment.

---

## 6. CloudFront with ALB and ECS/Fargate

**Architecture Flow**:
- User → AWS WAF → CloudFront → ALB → ECS/Fargate (Containerized frontend)

**Explanation**:
- **CloudFront** serves static assets and caches content globally.
- **AWS WAF** is applied to protect **CloudFront** from malicious requests.
- Dynamic frontend applications or SSR requests are forwarded from **CloudFront** to an **ALB**, which routes them to containerized applications running on **ECS** or **Fargate**.

**Benefits**:
- **Highly scalable**: **ECS/Fargate** can scale up or down based on demand, making it suitable for complex and high-traffic applications.
- **Flexibility**: Supports SSR and dynamic content, while **CloudFront** ensures fast delivery.
- **Security**: **AWS WAF** secures both the edge traffic via **CloudFront** and the backend services running on **ECS/Fargate**.

**Limitations**:
- **Complex setup**: Requires configuration of **ALB**, **ECS/Fargate**, and managing containerized applications, making it more complex to manage.
- **Cost**: The cost is higher compared to simpler solutions like **S3** + **CloudFront** due to the infrastructure needed for containers.

---

## 7. CloudFront with AWS Amplify

**Architecture Flow**:
- User → AWS WAF → CloudFront → AWS Amplify (Frontend hosting)

**Explanation**:
- **AWS Amplify** is a fully managed service that handles frontend hosting, CI/CD, and scaling automatically.
- **CloudFront** caches and distributes the content globally.
- **AWS WAF** is applied to **CloudFront** to protect against malicious requests.

**Benefits**:
- **Fully managed**: **Amplify** handles the deployment, scaling, and hosting of your frontend application, making it simple to use.
- **Integrated CI/CD**: Easy integration with CI/CD pipelines for frontend deployment.
- **Security**: **AWS WAF** protects the application against common web attacks.
- **Global Distribution**: **CloudFront** delivers content globally with low latency.

**Limitations**:
- **Limited flexibility**: **Amplify** supports only specific frameworks and workflows, limiting customization.
- **Cost**: May be more expensive than simpler static hosting options like **S3** + **CloudFront**.

---

## Comparison Table: Architecture Approaches

| **Architecture**                             | **Use Case**                                | **Benefits**                                                                                                                                                           | **Limitations**                                                                                                    |
|----------------------------------------------|---------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| **CloudFront + S3**                          | Static Frontends                            | Cost-effective, easy to set up, global distribution via **CloudFront**, secure with **AWS WAF**.                                                                      | Not suitable for dynamic content or SSR.                                                                          |
| **CloudFront + ALB + EC2/ECS/Fargate**       | Dynamic Frontends (SSR or backend)         | Scalable, flexible, global distribution, **AWS WAF** protection, suitable for complex frontend-backend applications.                                                   | Higher complexity, more expensive than static solutions.                                                           |
| **CloudFront + API Gateway**                 | API-centric Frontends                       | Centralized access for APIs, scalable, **AWS WAF** protection, API management features (throttling, validation), integrated with **Lambda**, **ECS**, or **EC2**.       | Slight latency due to **API Gateway**, potentially higher costs with high request volume.                          |
| **CloudFront + S3 + Lambda@Edge**            | Lightweight dynamic behavior at edge        | Fast, low-latency dynamic logic at edge, **AWS WAF** protection, global caching via **CloudFront**, cost-effective for simple logic.                                    | Limited compute and execution time for **Lambda@Edge**, not suitable for complex SSR.                             |
| **CloudFront + AWS App Runner**              | Containerized Frontends                     | Fully managed, automatic scaling, **AWS WAF** protection, cost-effective for containerized apps, simple setup.                                                         | Limited customization compared to **ECS/Fargate**, higher cost than static hosting.                               |
| **CloudFront + ALB + ECS/Fargate**           | Containerized Dynamic Frontends             | Highly scalable, flexible for SSR and dynamic content, **AWS WAF** protection, **CloudFront** caching, handles complex applications.                                   | Complex setup and management, higher cost than static hosting.                                                    |
| **CloudFront + AWS Amplify**                 | Frontend Hosting with CI/CD                 | Fully managed hosting, automatic scaling, **AWS WAF** protection, global distribution via **CloudFront**, easy integration with modern frontend frameworks.              | Limited to **Amplify** supported frameworks, potentially more expensive than basic static hosting.                |

---

### **Conclusion**

Choosing the right architecture depends on your application’s requirements. For static sites, **CloudFront + S3** is an excellent, cost-effective choice. For more complex, dynamic, or SSR-based applications, solutions like **CloudFront + ALB + ECS/Fargate** or **CloudFront + API Gateway** provide the scalability and flexibility required to handle backend logic.

Each approach provides its own set of **benefits** and **limitations**, so ensure that you assess the needs of your application, expected traffic, and security requirements before deciding.
