# **Kubernetes Security Enforcing Policies**

Kubernetes security policies help protect clusters from misconfigurations, unauthorized access, and security risks. These policies can be implemented using **Kyverno**, **OPA Gatekeeper**, or built-in Kubernetes security features.

### **Security Policy Categories**

| **Category**           | **Policy Type**            | **Purpose** |
|-----------------------|--------------------------|------------|
| **Pod Security**      | Pod Security Admission (PSA) | Restrict privilege escalation, enforce securityContext |
| **Network Security**  | Network Policies | Control pod-to-pod communication |
| **Authentication & Authorization** | RBAC (Role-Based Access Control) | Limit access based on user roles |
| **Image Security**    | Image Admission Policies | Prevent usage of untrusted or `latest` images |
| **Runtime Security**  | PodSecurityPolicies (Deprecated) / Seccomp & AppArmor | Restrict capabilities & enforce seccomp profiles |
| **Resource Quotas & Limits** | Resource Quotas & LimitRanges | Prevent excessive resource usage |
| **Data Security**     | Encryption Policies | Encrypt secrets at rest and enforce access controls |
| **Audit & Monitoring** | Logging & Policy Reports | Track security violations and audit cluster events |

---

## **Pod Security Policies (PSA)**

**Purpose:** Restrict Pod privileges and enforce security best practices.  
**Implementation:** Pod Security Admission (PSA) (since Kubernetes 1.25, replaces PSP).  
**Enforcement Levels:**
- Privileged (No restrictions)
- Baseline (Blocks privilege escalation)
- Restricted (Strong security enforcement)

**Example: Enforcing Restricted PSA**
```yaml
apiVersion: policy/v1
kind: PodSecurityPolicy
metadata:
  name: restricted-psp
spec:
  privileged: false
  allowPrivilegeEscalation: false
  runAsUser:
    rule: MustRunAsNonRoot
  seLinux:
    rule: RunAsAny
  fsGroup:
    rule: MustRunAs
    ranges:
      - min: 1
        max: 65535
  volumes:
    - 'configMap'
    - 'emptyDir'
```

Alternative: Use **Kyverno** to enforce similar rules.

---

## **Network Policies**

**Purpose:** Restrict network traffic between Pods.  
**Implementation:** Kubernetes **NetworkPolicy** objects.

**Example: Deny All Traffic by Default**
```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: default-deny
  namespace: default
spec:
  podSelector: {}
  policyTypes:
    - Ingress
    - Egress
```

**Example: Allow Only Traffic from Specific App**
```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-app
spec:
  podSelector:
    matchLabels:
      app: web
  ingress:
    - from:
        - podSelector:
            matchLabels:
              app: backend
```

---

## **RBAC (Role-Based Access Control)**

**Purpose:** Restrict access to Kubernetes resources based on user roles.  
**Implementation:** Define **Roles** and **RoleBindings**.

**Example: Read-Only Access to Pods**
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: pod-reader
rules:
  - apiGroups: [""]
    resources: ["pods"]
    verbs: ["get", "list", "watch"]
```
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: read-only-binding
subjects:
  - kind: User
    name: alice
    apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```

---

## **Image Security Policies**

**Purpose:** Prevent deployment of vulnerable, untrusted, or `latest` tag images.  
**Implementation:** Kyverno or OPA Gatekeeper.

**Example: Block `latest` Image Tags with Kyverno**
```yaml
apiVersion: kyverno.io/v1
kind: ClusterPolicy
metadata:
  name: disallow-latest-tag
spec:
  validationFailureAction: Enforce
  rules:
    - name: validate-image-tag
      match:
        resources:
          kinds:
            - Pod
      validate:
        message: "Using 'latest' tag is not allowed"
        pattern:
          spec:
            containers:
              - image: "!*:latest"
```

**Example: Allow Only Signed Images (Sigstore Cosign)**
```yaml
apiVersion: kyverno.io/v1
kind: ClusterPolicy
metadata:
  name: verify-signed-images
spec:
  validationFailureAction: Enforce
  rules:
    - name: check-image-signature
      match:
        resources:
          kinds:
            - Pod
      verifyImages:
        - imageReferences:
            - "registry.myorg.com/*"
          attestors:
            - entries:
                - keys:
                    publicKeys: |
                      -----BEGIN PUBLIC KEY-----
                      YOUR-PUBLIC-KEY
                      -----END PUBLIC KEY-----
```

---

## **Runtime Security**

**Purpose:** Restrict runtime capabilities of containers (e.g., disable privilege escalation).  
**Implementation:** Seccomp, AppArmor, and Kyverno.

**Example: Enforce Seccomp Profile**
```yaml
apiVersion: kyverno.io/v1
kind: ClusterPolicy
metadata:
  name: enforce-seccomp
spec:
  validationFailureAction: Enforce
  rules:
    - name: check-seccomp
      match:
        resources:
          kinds:
            - Pod
      validate:
        message: "Seccomp must be set to runtime/default"
        pattern:
          spec:
            securityContext:
              seccompProfile:
                type: "RuntimeDefault"
```

---

## **Resource Quotas & Limits**

**Purpose:** Prevent excessive resource consumption and DoS attacks.  
**Implementation:** Kubernetes **LimitRanges** and **ResourceQuotas**.

**Example: Set Resource Limits**
```yaml
apiVersion: v1
kind: LimitRange
metadata:
  name: container-limits
spec:
  limits:
    - default:
        cpu: 500m
        memory: 512Mi
      defaultRequest:
        cpu: 250m
        memory: 256Mi
      type: Container
```

---

## **Data Security Policies**

**Purpose:** Encrypt Kubernetes Secrets and restrict access.  
**Implementation:** KMS encryption, Kyverno policies.

**Example: Enforce Secret Encryption**
```yaml
apiVersion: kyverno.io/v1
kind: ClusterPolicy
metadata:
  name: enforce-secret-encryption
spec:
  validationFailureAction: Enforce
  rules:
    - name: check-secret-encryption
      match:
        resources:
          kinds:
            - Secret
      validate:
        message: "Secrets must be encrypted at rest"
        deny:
          conditions:
            - key: "{{request.object.metadata.annotations.kms-encrypted}}"
              operator: Equals
              value: "false"
```

---

## **Conclusion**

Security enforcement policies help protect Kubernetes clusters by restricting access, preventing vulnerabilities, and ensuring compliance. **Kyverno** and **OPA Gatekeeper** provide powerful policy enforcement for security, while built-in Kubernetes features like RBAC and NetworkPolicies offer essential protections. **Implementing multiple layers of security policies** ensures a **Zero Trust Kubernetes environment**.
