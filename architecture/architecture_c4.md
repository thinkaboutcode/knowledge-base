# 4C Model for Software Architecture

The **4C Model for Software Architecture** by Simon Brown provides a simple, hierarchical approach to visualize and communicate the architecture of a software system. It focuses on different levels of detail: **Context**, **Containers**, **Components**, and **Code**.

---

## 1. Context Diagram (System Context)
- **Purpose**: High-level view showing the system’s relationship with external actors (users, external systems).
- **Focus**: **Who** uses the system and **how** it interacts with other systems.
- **Key Elements**:
    - **System Boundary**: Defines what is inside and outside the system.
    - **Actors**: Users or external systems that interact with the system.
    - **External Systems**: Systems outside your architecture.
- **Diagram**: Simple overview with arrows pointing between the system and external actors/systems.

---

## 2. Containers Diagram
- **Purpose**: Shows the high-level building blocks (applications, services, databases) and their communication.
- **Focus**: **Where** code runs and **how** containers communicate.
- **Key Elements**:
    - **Containers**: Deployable/executable units (applications, services, databases).
    - **Technology Stack**: Shows technology used in each container (e.g., Java app, SQL database).
    - **Inter-Container Communication**: Arrows representing protocols (e.g., HTTP, SQL).
- **Diagram**: Containers as boxes, with lines/arrows showing interactions between them.

---

## 3. Components Diagram
- **Purpose**: Shows the internal structure of each container, breaking it into components (modules, services).
- **Focus**: **What** major components exist inside each container and how they interact.
- **Key Elements**:
    - **Components**: Major building blocks inside a container.
    - **Responsibilities**: The function of each component (e.g., service layers, database access).
    - **Inter-Component Communication**: Interaction between components inside a container.
- **Diagram**: Shows internal components of a container, with labeled interactions between them.

---

## 4. Code (Class) Diagram
- **Purpose**: Detailed view showing the implementation of components at the code level (classes, methods).
- **Focus**: **How** a component is implemented with code.
- **Key Elements**:
    - **Classes**: Detailed class or object structure (e.g., class methods, properties).
    - **Relationships**: Inheritance, associations between classes.
    - **Implementation Details**: Showing how the system is built with code.
- **Diagram**: UML-style class diagrams or detailed pseudo-code view.

---

### Key Principles of the 4C Model
- **Abstraction**: Diagrams provide different levels of abstraction—from high-level system interaction to low-level code.
- **Communication**: Use diagrams to facilitate communication between technical and non-technical stakeholders.
- **Zoom-in Structure**: Each diagram zooms into more detail from the previous one.

### Links
- [Simon Brown's 4C Model](https://c4model.com/)
