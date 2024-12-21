# Clean Architecture Cheat Sheet

## Overview
Clean Architecture is a layered approach to software design that separates concerns, making the system flexible, testable, and maintainable. The goal is to decouple business logic from frameworks, UI, databases, and other external concerns.

---

## Core Principles

1. **Separation of Concerns**: Each layer is responsible for a specific role.
2. **Single Responsibility Principle (SRP)**: A module/class should have one reason to change.
3. **Open/Closed Principle (OCP)**: Modules should be open for extension but closed for modification.
4. **Liskov Substitution Principle (LSP)**: Subtypes must be substitutable for their base types.
5. **Interface Segregation Principle (ISP)**: Clients should not be forced to depend on interfaces they do not use.
6. **Dependency Inversion**: High-level modules should not depend on low-level modules. Both should depend on abstractions (interfaces).

---

## Layers of Clean Architecture

<img src="architecture_clean.jpg" alt="clean architecture" />

### 1. **Entities**
- **Description**: Business logic and rules. Independent of any external component (framework, database, etc.).
- **Role**: Define the core business rules or data models.
- **Dependency**: Depends on nothing.

### 2. **Use Cases (Interactors)**
- **Description**: Application-specific business rules. Defines what the software does.
- **Role**: Orchestrate the flow between entities and external components.
- **Dependency**: Can depend on entities, but should not depend on UI, database, or frameworks.

### 3. **Interface Adapters (Controllers, Presenters, Gateways)**
- **Description**: Converts data between the core application and the external systems (UI, DB, etc.).
- **Role**: Present data to the user, fetch from API, interact with databases, etc.
- **Dependency**: Depends on use cases and entities but can also communicate with external systems.

### 4. **Frameworks & Drivers (UI, DB, Web, etc.)**
- **Description**: External components like web frameworks, databases, UI.
- **Role**: Act as the delivery mechanism.
- **Dependency**: Should only depend on the layer above them (interface adapters).

---

## Dependency Rule

**Dependencies only point inward.**  
Higher-level layers (e.g., frameworks) can depend on lower-level layers (e.g., interface adapters, use cases) but **never** the reverse.

---

## Data Flow

1. **Entities**: Contains core logic.
2. **Use Cases**: Invokes entities and applies the business rules.
3. **Interface Adapters**: Adapts data for external or internal communication.
4. **Frameworks**: External systems interacting via interface adapters.

---

## Key Practices

1. **Use Dependency Injection**: Abstract the concrete dependencies (e.g., repositories, services) to keep the business logic independent.
2. **Keep UI Frameworks Isolated**: The UI should know nothing about the business logic.
3. **Use Boundaries**: Define interfaces to isolate dependencies across layers.
4. **Testability**: Core logic (entities, use cases) should be independently testable without the external systems.
5. **Avoid Circular Dependencies**: Ensure that no circular dependencies are introduced between layers.

---

## Code Example (Simple Structure)

```text
src/
├── entities/
│   └── user.py
├── usecases/
│   └── create_user.py
├── interface_adapters/
│   ├── controllers/
│   │   └── user_controller.py
│   └── repositories/
│       └── user_repository.py
├── frameworks/
│   ├── web/
│   │   └── flask_server.py
│   └── database/
│       └── sql_database.py
└── main.py
```

## Key Benefits
- **Independent of Frameworks**: You can replace frameworks easily without impacting the core business logic.
- **Testable**: Business rules can be tested without UI, database, or external dependencies.
- **Independent of UI**: The user interface can change without affecting the system's core logic.
- **Independent of Database**: The data layer can be swapped out without changing business rules.
- **Independent of any external agency**: The system remains independent from external systems such as UI, databases, and third-party APIs.

---

## References
- **Clean Architecture: A Craftsman's Guide to Software Structure and Design** by Robert C. Martin
- **SOLID Principles**: The foundation of Clean Architecture design

