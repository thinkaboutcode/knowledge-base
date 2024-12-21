# Kubectl Cheat Sheet

## Kubernetes Context and Configuration

| **Command**                                     | **Description**                                                    |
|-------------------------------------------------|--------------------------------------------------------------------|
| `kubectl config view`                           | View the current Kubernetes configuration.                         |
| `kubectl config current-context`                | Display the current context.                                       |
| `kubectl config use-context [context-name]`     | Switch to a different context.                                     |
| `kubectl config get-contexts`                   | List all available contexts.                                       |
| `kubectl config set-context [context-name] --namespace=[namespace]` | Set a default namespace for a context. |

## Working with Namespaces

| **Command**                     | **Description**                                                    |
|---------------------------------|--------------------------------------------------------------------|
| `kubectl get namespaces`        | List all namespaces in the cluster.                                |
| `kubectl create namespace [name]` | Create a new namespace.                                          |
| `kubectl delete namespace [name]` | Delete a namespace and all resources within it.                 |
| `kubectl config set-context --current --namespace=[namespace]` | Set a default namespace in the current context. |

## Pod Management

| **Command**                     | **Description**                                                    |
|---------------------------------|--------------------------------------------------------------------|
| `kubectl get pods`              | List all pods in the current namespace.                            |
| `kubectl get pods -n [namespace]` | List all pods in a specific namespace.                           |
| `kubectl describe pod [pod-name]` | Display detailed information about a specific pod.              |
| `kubectl logs [pod-name]`       | View the logs of a specific pod.                                   |
| `kubectl logs -f [pod-name]`    | Stream the logs of a specific pod.                                 |
| `kubectl exec -it [pod-name] -- /bin/bash` | Start an interactive shell session inside a pod.               |
| `kubectl delete pod [pod-name]` | Delete a specific pod.                                             |
| `kubectl get pod [pod-name] -o yaml` | Get the YAML configuration of a specific pod.               |

## Service Management

| **Command**                     | **Description**                                                    |
|---------------------------------|--------------------------------------------------------------------|
| `kubectl get services`          | List all services in the current namespace.                        |
| `kubectl get svc`               | Shortcut for listing services (svc = services).                    |
| `kubectl describe service [service-name]` | Display detailed information about a specific service.      |
| `kubectl expose pod [pod-name] --port=[port] --target-port=[target-port] --name=[service-name]` | Create a service for a specific pod. |
| `kubectl delete service [service-name]` | Delete a specific service.                                      |

## Deployment Management

| **Command**                     | **Description**                                                    |
|---------------------------------|--------------------------------------------------------------------|
| `kubectl get deployments`       | List all deployments in the current namespace.                     |
| `kubectl get deployment [deployment-name]` | Get details about a specific deployment.                     |
| `kubectl describe deployment [deployment-name]` | Display detailed information about a specific deployment.  |
| `kubectl create deployment [deployment-name] --image=[image-name]` | Create a new deployment using a specific image. |
| `kubectl scale deployment [deployment-name] --replicas=[number]` | Scale a deployment to a specific number of replicas.        |
| `kubectl delete deployment [deployment-name]` | Delete a specific deployment.                                |
| `kubectl set image deployment/[deployment-name] [container-name]=[new-image:tag]` | Update the image of a deployment. |

## ReplicaSet Management

| **Command**                     | **Description**                                                    |
|---------------------------------|--------------------------------------------------------------------|
| `kubectl get replicasets`       | List all ReplicaSets in the current namespace.                     |
| `kubectl describe rs [replicaset-name]` | Display detailed information about a specific ReplicaSet.   |
| `kubectl scale rs [replicaset-name] --replicas=[number]` | Scale a ReplicaSet to a specific number of replicas.       |
| `kubectl delete rs [replicaset-name]` | Delete a specific ReplicaSet.                                    |

## Job and CronJob Management

| **Command**                     | **Description**                                                    |
|---------------------------------|--------------------------------------------------------------------|
| `kubectl get jobs`              | List all jobs in the current namespace.                            |
| `kubectl describe job [job-name]` | Display detailed information about a specific job.              |
| `kubectl delete job [job-name]` | Delete a specific job.                                             |
| `kubectl get cronjobs`          | List all CronJobs in the current namespace.                        |
| `kubectl describe cronjob [cronjob-name]` | Display detailed information about a specific CronJob.       |
| `kubectl delete cronjob [cronjob-name]` | Delete a specific CronJob.                                    |

## ConfigMaps and Secrets

| **Command**                     | **Description**                                                    |
|---------------------------------|--------------------------------------------------------------------|
| `kubectl create configmap [name] --from-literal=[key]=[value]` | Create a ConfigMap from literal values.                 |
| `kubectl create configmap [name] --from-file=[file-path]` | Create a ConfigMap from a file.                                |
| `kubectl get configmaps`        | List all ConfigMaps in the current namespace.                      |
| `kubectl describe configmap [name]` | Display detailed information about a specific ConfigMap.     |
| `kubectl delete configmap [name]` | Delete a specific ConfigMap.                                     |
| `kubectl create secret generic [name] --from-literal=[key]=[value]` | Create a secret from literal values.            |
| `kubectl create secret generic [name] --from-file=[file-path]` | Create a secret from a file.                               |
| `kubectl get secrets`           | List all secrets in the current namespace.                         |
| `kubectl describe secret [name]` | Display detailed information about a specific secret.            |
| `kubectl delete secret [name]`  | Delete a specific secret.                                          |

## Resource Management

| **Command**                     | **Description**                                                    |
|---------------------------------|--------------------------------------------------------------------|
| `kubectl get all`               | List all resources in the current namespace.                       |
| `kubectl get [resource]`        | List a specific type of resource (e.g., pods, services).           |
| `kubectl describe [resource] [name]` | Display detailed information about a specific resource.       |
| `kubectl delete [resource] [name]` | Delete a specific resource.                                      |
| `kubectl apply -f [file.yaml]`  | Apply a configuration file to create or update resources.          |
| `kubectl delete -f [file.yaml]` | Delete resources defined in a configuration file.                  |
| `kubectl get [resource] -o wide` | Get a specific resource with additional details.                 |
| `kubectl get [resource] -o yaml` | Get the YAML configuration of a resource.                        |

## Rolling Updates and Rollbacks

| **Command**                     | **Description**                                                    |
|---------------------------------|--------------------------------------------------------------------|
| `kubectl rollout status deployment/[deployment-name]` | Check the status of a deployment rollout.                |
| `kubectl rollout history deployment/[deployment-name]` | View the history of a deployment’s rollouts.            |
| `kubectl rollout undo deployment/[deployment-name]` | Rollback to the previous version of a deployment.          |
| `kubectl set image deployment/[deployment-name] [container-name]=[new-image:tag]` | Perform a rolling update by changing the image. |
| `kubectl rollout pause deployment/[deployment-name]` | Pause a deployment's rollout.                                |
| `kubectl rollout resume deployment/[deployment-name]` | Resume a paused deployment's rollout.                        |

## Monitoring and Troubleshooting

| **Command**                     | **Description**                                                    |
|---------------------------------|--------------------------------------------------------------------|
| `kubectl top nodes`             | Display resource usage (CPU/memory) of nodes.                      |
| `kubectl top pods`              | Display resource usage (CPU/memory) of pods.                       |
| `kubectl describe [resource] [name]` | Display detailed information, including events, for a specific resource. |
| `kubectl logs [pod-name]`       | View the logs of a specific pod.                                   |
| `kubectl logs -f [pod-name]`    | Stream the logs of a specific pod.                                 |
| `kubectl exec -it [pod-name] -- [command]` | Execute a command in a running pod.                         |
| `kubectl get events`            | List all events in the current namespace.                          |
| `kubectl describe node [node-name]` | Display detailed information about a specific node.            |
| `kubectl get componentstatuses` | Check the status of the cluster components.                        |

## Advanced Commands

| **Command**                     | **Description**                                                    |
|---------------------------------|--------------------------------------------------------------------|
| `kubectl apply -f [dir/]`       | Apply all YAML files in a directory.                               |
| `kubectl port-forward [pod-name] [local-port]:[pod-port]` | Forward one or more local ports to a pod.            |
| `kubectl proxy`                 | Start a proxy to the Kubernetes API server.                        |
| `kubectl edit [resource] [name]` | Edit a resource in place using the default editor.                |
| `kubectl label [resource] [name] [key]=[value]` | Add or update labels on a resource.                          |
| `kubectl annotate [resource] [name] [key]=[value]` | Add or update annotations on a resource.                    |
| `kubectl cordon [node-name]`    | Mark a node as unschedulable.                                      |
| `kubectl drain [node-name]`     | Drain a node by evicting all pods.                                 |
| `kubectl uncordon [node-name]`  | Mark a node as schedulable again.                                  |

