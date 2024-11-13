# Validating and Mutating Webhooks in Kubernetes

In Kubernetes, **Validating Webhooks** and **Mutating Webhooks** are part of the **Admission Control** mechanism. They help manage and enforce custom policies on resources before they are persisted in the cluster. These webhooks allow for validation of incoming requests and automatic mutation of resource definitions based on specific rules.

---

## 1. Validating Webhooks

A **Validating Webhook** is used to **validate** the incoming Kubernetes API request. It enforces custom validation rules and rejects requests that do not meet specified criteria.

### How It Works:
- When a request (such as creating or modifying a resource) is made to the Kubernetes API server, it goes through the admission control process.
- If a validating webhook is configured, Kubernetes sends the resource definition to the webhook server for validation.
- The webhook evaluates the request based on custom logic (e.g., checking configurations, security policies, or resource limits).
- If the webhook returns a **deny** response, the resource creation or update is rejected.
- If the webhook returns an **accept** response (or no response), the request proceeds as usual.

### Use Cases:
- Enforcing custom policies on resource creation (e.g., ensuring resources do not exceed certain limits).
- Enforcing security rules (e.g., requiring specific labels on namespaces or enforcing image policies).
- Ensuring that only specific users or service accounts can create certain types of resources.

---

## 2. Mutating Webhooks

A **Mutating Webhook** allows you to **mutate** or modify the resource definition before it is persisted in the cluster. This means the webhook can automatically adjust the resource configuration (such as adding labels, annotations, or modifying resource requests).

### How It Works:
- When a request is made to the Kubernetes API, the resource passes through the admission control process.
- If a mutating webhook is configured, Kubernetes sends the resource to the webhook server for mutation.
- The webhook server can modify the resource definition (e.g., add labels, change container configurations, or set default values).
- Once the resource is mutated, it is returned to the API server, which processes the request as usual.

### Use Cases:
- Automatically injecting sidecar containers into Pods (e.g., for monitoring or logging).
- Adding default values to missing fields (e.g., setting a default image pull policy).
- Injecting specific security-related configurations into resources (e.g., ensuring that all pods have a specific security context).

---

## Key Differences Between Validating and Mutating Webhooks

| Feature                         | **Validating Webhooks**                              | **Mutating Webhooks**                                 |
|----------------------------------|------------------------------------------------------|------------------------------------------------------|
| **Purpose**                      | To **validate** requests before they are persisted.  | To **mutate** or **modify** requests before they are persisted. |
| **Operation**                    | Rejects or accepts the request based on custom logic. | Modifies the request and returns the modified resource. |
| **Use Case**                     | Enforcing custom validation rules (e.g., security policies, naming conventions). | Automatically injecting defaults, adding labels, or enforcing security-related configurations. |
| **Response**                     | Return an acceptance or rejection (allow or deny).   | Return the modified resource after the mutation.      |
| **Order of Execution**           | Executed after mutating webhooks and before the resource is persisted. | Executed first, before validating webhooks and before persistence. |

---

## Webhook Admission Control Flow

1. **Mutating Webhooks**: If mutating webhooks are configured, they are executed first. These webhooks modify the resource as needed and return the mutated resource to the API server.
2. **Validating Webhooks**: After mutating webhooks, validating webhooks are executed. They verify that the resource adheres to custom rules and either accept or reject the resource.
3. **Persistence**: If the resource passes both validation and mutation (if applicable), it is persisted in the cluster.

---

## How to Configure Webhooks in Kubernetes

Both **Validating** and **Mutating Webhooks** are configured using **Admission Webhook Resources** in Kubernetes.

1. **Define a Webhook Server**: This server listens for requests from the Kubernetes API server, processes the resource data, and returns either a validation or mutated response.
2. **Create a Webhook Configuration**:
    - `MutatingWebhookConfiguration`: For mutating webhooks.
    - `ValidatingWebhookConfiguration`: For validating webhooks.
3. **Configure the Kubernetes API Server**: The API server must be configured to call your webhook server for the relevant resource operations.

---

## Security Considerations

- **TLS Security**: Both mutating and validating webhooks must communicate over HTTPS to ensure the integrity and security of the data being transferred.
- **Webhook Timeout**: Webhook servers must respond promptly to avoid delays in processing the API request. Kubernetes has a configurable timeout for webhooks.
- **Webhook Failure**: If a webhook fails (e.g., network issues or misconfiguration), it may cause the request to be rejected, depending on the `failurePolicy` setting (either `Fail` or `Ignore`).

---

## Conclusion

- **Validating Webhooks** are primarily used for **validation**, ensuring that incoming requests conform to required policies before being accepted.
- **Mutating Webhooks** are used to **mutate** or modify requests before they are persisted, allowing you to automatically modify or enhance resources based on specific needs.

Together, these webhooks provide a powerful way to enforce policies, automate configuration tasks, and ensure the security and integrity of Kubernetes clusters.
