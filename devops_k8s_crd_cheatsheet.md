# Custom Resource Definitions (CRDs) in Kubernetes

In Kubernetes, **Custom Resource Definitions (CRDs)** allow users to extend the Kubernetes API to create custom resources (CRs) tailored to specific applications or infrastructure needs. By defining a CRD, you can manage additional resource types beyond the default ones (like Pods or Services) as if they were native to Kubernetes.

### How CRDs Work

1. **Define the Custom Resource (CR)**:
    - A CRD specifies the schema for a new resource, including fields, types, and validation rules.
    - Once a CRD is applied to the cluster, users can create custom resources (CRs) based on this schema.

2. **Interaction with Kubernetes API**:
    - After creating a CRD, the Kubernetes API is automatically extended to include the new resource type.
    - Users interact with these custom resources using `kubectl` commands (`kubectl get <resource>`, `kubectl apply -f <resource>.yaml`), just like any standard Kubernetes object.

3. **Controller Integration**:
    - CRDs are often paired with custom controllers, which monitor and manage the lifecycle of these resources.
    - These controllers implement logic to respond to changes in the CR, orchestrating custom behavior as required by the application.

### Example CRD and Custom Resource

Here’s a simple example of a CRD for an `ExampleResource`, representing a basic resource that stores a greeting message.

1. **Define the CRD (example_resource_crd.yaml)**:

    ```yaml
    apiVersion: apiextensions.k8s.io/v1
    kind: CustomResourceDefinition
    metadata:
      name: exampleresources.example.com
    spec:
      group: example.com
      versions:
        - name: v1
          served: true
          storage: true
          schema:
            openAPIV3Schema:
              type: object
              properties:
                spec:
                  type: object
                  properties:
                    message:
                      type: string
                      description: "A greeting message"
      scope: Namespaced
      names:
        plural: exampleresources
        singular: exampleresource
        kind: ExampleResource
        shortNames:
          - exr
    ```

    - This YAML defines a new resource type `ExampleResource` with a single field, `message`.

2. **Create an Instance of the Custom Resource (example_resource.yaml)**:

    ```yaml
    apiVersion: example.com/v1
    kind: ExampleResource
    metadata:
      name: hello-world
    spec:
      message: "Hello, Kubernetes!"
    ```

    - This YAML creates an instance of `ExampleResource` with the name `hello-world` and a message "Hello, Kubernetes!".

3. **Apply the CRD and Custom Resource**:

    ```bash
    kubectl apply -f example_resource_crd.yaml
    kubectl apply -f example_resource.yaml
    ```

4. **Check the Custom Resource**:

    ```bash
    kubectl get exampleresources
    kubectl get exampleresource hello-world -o yaml
    ```

This simple setup defines a custom resource type (`ExampleResource`) and creates an instance of it. When paired with a custom controller, Kubernetes can monitor this resource and trigger specific actions based on its state.

