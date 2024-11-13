classDiagram
class Pod {
+String name
+String status
+String namespace
+Container[] containers
+Volume[] volumes
+ServiceAccount serviceAccount
}

    class Deployment {
        +String name
        +PodTemplateSpec podTemplate
        +int replicas
        +String namespace
        +Pod[] pods
        +LabelSelector selector
    }

    class Service {
        +String name
        +String type
        +String namespace
        +PodSelector selector
        +Port[] ports
        +String clusterIP
    }

    class Namespace {
        +String name
        +Pod[] pods
        +Service[] services
        +Volume[] volumes
    }

    class Volume {
        +String name
        +String type
        +String mountPath
    }

    class Container {
        +String name
        +String image
        +String command
        +String[] env
        +String[] ports
    }

    class ServiceAccount {
        +String name
        +Secret[] secrets
        +Role[] roles
    }

    class LabelSelector {
        +String[] labels
    }

    class PodTemplateSpec {
        +Container[] containers
        +Volume[] volumes
    }

    class Port {
        +int port
        +int targetPort
    }

    class Secret {
        +String name
        +String[] data
    }

    class Role {
        +String name
        +String[] permissions
    }

    Pod "1" --> "0..*" Container : contains
    Pod "1" --> "0..*" Volume : mounts
    Deployment "1" --> "1" PodTemplateSpec : defines
    Deployment "1" --> "0..*" Pod : manages
    Service "1" --> "0..*" Pod : targets
    Service "1" --> "0..*" Port : exposes
    Namespace "1" --> "0..*" Pod : contains
    Namespace "1" --> "0..*" Service : contains
    Namespace "1" --> "0..*" Volume : contains
    ServiceAccount "1" --> "0..*" Secret : uses
    ServiceAccount "1" --> "0..*" Role : assigned
    Pod "0..*" --> "0..1" ServiceAccount : uses
