# Overview of Reactor, WebFlux, and R2DBC with Sample Java Application

## Overview of Technologies

### 1. Reactor
- **Description**: Reactor is a reactive programming library for building non-blocking applications on the JVM. It is part of the larger Spring ecosystem and provides a foundation for handling asynchronous data streams.
- **Core Components**:
    - **Mono**: Represents a sequence of 0 or 1 item.
    - **Flux**: Represents a sequence of 0 to N items.
- **Features**:
    - Support for backpressure, enabling better control over data flow.
    - Operators for transforming, filtering, and combining data streams.
    - Integration with various data sources and libraries.

### 2. WebFlux
- **Description**: Spring WebFlux is a reactive web framework that is part of the Spring Framework, designed to handle asynchronous requests and responses. It leverages Reactor to provide a non-blocking architecture.
- **Core Features**:
    - Annotations similar to Spring MVC (like `@RestController`, `@RequestMapping`) but for reactive programming.
    - Supports multiple runtime environments, including Netty and Servlet 3.1+ containers.
    - Handles reactive types (Mono and Flux) as return types for request handling.

### 3. R2DBC (Reactive Relational Database Connectivity)
- **Description**: R2DBC is an API specification for reactive programming with relational databases. It allows for non-blocking interactions with SQL databases, making it easier to build reactive applications.
- **Core Features**:
    - Provides reactive types for querying and interacting with databases (similar to Mono and Flux).
    - Support for various databases via drivers (like PostgreSQL, MySQL, etc.).
    - Enables backpressure and stream processing with database operations.

## Sample Application

This sample application demonstrates a simple REST API using Spring WebFlux and R2DBC to interact with a PostgreSQL database.

### Prerequisites
- Java 11 or higher
- Maven
- PostgreSQL database

### Project Setup

1. **Add Dependencies** in `pom.xml`:
   ```xml
   <dependencies>
       <dependency>
           <groupId>org.springframework.boot</groupId>
           <artifactId>spring-boot-starter-data-r2dbc</artifactId>
       </dependency>
       <dependency>
           <groupId>org.springframework.boot</groupId>
           <artifactId>spring-boot-starter-webflux</artifactId>
       </dependency>
       <dependency>
           <groupId>io.r2dbc</groupId>
           <artifactId>r2dbc-postgresql</artifactId>
       </dependency>
       <dependency>
           <groupId>org.springframework.boot</groupId>
           <artifactId>spring-boot-starter-test</artifactId>
           <scope>test</scope>
       </dependency>
   </dependencies>
    ```

2. Configuration in `application.yml`

    To configure the application, create an `application.yml` file in the `src/main/resources` directory and add the following content:

    ```yaml
    spring:
      r2dbc:
        url: r2dbc:postgresql://localhost:5432/mydb
        username: myuser
        password: mypassword
      datasource:
        driver-class-name: org.postgresql.Driver
    ```

3. Create a Domain Model

    In this step, we will define a domain model class named `User` that represents the users in our application. The class will include fields for the user ID and name, as well as appropriate annotations for mapping to the database

    ```java
    import org.springframework.data.annotation.Id;
    import org.springframework.data.relational.core.mapping.Table;
    
    @Table("users") // Specifies the table name in the database
    public class User {
        @Id // Indicates that this field is the primary key
        private Long id;
        private String name;
    
        // Getter for id
        public Long getId() {
            return id;
        }
    
        // Setter for id
        public void setId(Long id) {
            this.id = id;
        }
    
        // Getter for name
        public String getName() {
            return name;
        }
    
        // Setter for name
        public void setName(String name) {
            this.name = name;
        }
    }
    ```

4. Create a Repository Interface

   In this step, you will create a repository interface that extends `ReactiveCrudRepository`. This interface will provide CRUD operations for the `User` entity without needing to implement any methods manually.

    ```java
    import org.springframework.data.repository.reactive.ReactiveCrudRepository;
    
    public interface UserRepository extends ReactiveCrudRepository<User, Long> {
    }
    ```

5. Create a REST Controller

    In this step, you'll create a REST controller to handle HTTP requests for user operations.

    ```java
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.http.HttpStatus;
    import org.springframework.http.ResponseEntity;
    import org.springframework.web.bind.annotation.*;
    import reactor.core.publisher.Flux;
    import reactor.core.publisher.Mono;
    
    @RestController
    @RequestMapping("/users")
    public class UserController {
    
        @Autowired
        private UserRepository userRepository;
    
        @GetMapping
        public Flux<User> getAllUsers() {
            return userRepository.findAll();
        }
    
        @GetMapping("/{id}")
        public Mono<ResponseEntity<User>> getUserById(@PathVariable Long id) {
            return userRepository.findById(id)
                    .map(user -> ResponseEntity.ok(user))
                    .defaultIfEmpty(ResponseEntity.notFound().build());
        }
    
        @PostMapping
        public Mono<User> createUser(@RequestBody User user) {
            return userRepository.save(user);
        }
    }
    ```

6. Application Entry Point

    In this section, you define the main application class to bootstrap the Spring Boot application. This class is annotated with `@SpringBootApplication`, which combines several other annotations including `@Configuration`, `@EnableAutoConfiguration`, and `@ComponentScan`.

    ```java
    import org.springframework.boot.SpringApplication;
    import org.springframework.boot.autoconfigure.SpringBootApplication;
    
    @SpringBootApplication
    public class ReactiveApplication {
        public static void main(String[] args) {
            SpringApplication.run(ReactiveApplication.class, args);
        }
    }
    ```

7. How to Run the Application

   1. **Set Up the Database**:
      Create a PostgreSQL database named `mydb` and a `users` table with the following SQL command:
      ```sql
      CREATE TABLE users (
          id SERIAL PRIMARY KEY,
          name VARCHAR(255) NOT NULL
      );
      ```
   
   2. **Run the Application**:
   Use Maven to build and run the application:
   ```bash
   mvn spring-boot:run
   ```

   3. Test the Endpoints
   You can use tools like Postman or curl to test the endpoints:

   - **GET** `/users` to retrieve all users.
   - **GET** `/users/{id}` to retrieve a user by ID.
   - **POST** `/users` with a JSON body to create a new user. For example:
     ```json
     {
         "name": "John Doe"
     }
     ```









