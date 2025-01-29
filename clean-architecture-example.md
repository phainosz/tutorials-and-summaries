# Clean Architecture - Example

## 📌 Overview
This document explains the data flow in a Clean Architecture project by implementing a simple **Find User by ID** use case.

### **Project Structure**
```
src/main/java/com/example/cleanarchitecture
├── core
│   ├── domain
│   ├── usecase
│   ├── exception
│   └── gateway
├── dataprovider
│   ├── repository
│   │   ├── entity
│   │   ├── jpa
│   │   └── custom
│   ├── mapper
│   ├── gateway
│   ├── rest
│   │   ├── client
│   │   ├── dto
│   │   └── mapper
│   └── messaging
│       ├── kafka
│       │   ├── consumer
│       │   ├── producer
│       │   └── config
├── entrypoint
│   ├── controller
│   ├── dto
│   ├── mapper
├── config
```

## Layers and Responsabilities

## 1. Core (Business Rules)

The "core" represents the domain and pure business rules, with no external dependencies.  

### 📂 `core/domain`
- Contains business entities.
- Simple classes (POJOs) that model the essential concepts of the system.
- Should be independent of frameworks and persistence.

### 📂 `core/usecase`
- Contains use cases (Application Business Rules).
- Defines application rules and orchestrates interactions between entities and gateways.
- Typically follows the "Interactor" pattern and uses interfaces for dependencies.

### 📂 `core/exception`
- Defines custom domain exceptions.
- Example: `UserNotFoundException`, `InvalidOrderException`.

### 📂 `core/gateway`
- Defines interfaces for accessing external data sources (databases, APIs, queues).
- Example: `UserGateway` with methods like `findById`, `save`, `deleteById`.

---

## 2. Data Provider (Gateway Implementations)

This layer implements the contracts defined in `core/gateway` and deals with infrastructure details.  

### 📂 `dataprovider/repository`
- Handles data persistence.

### 📂 `dataprovider/repository/entity`
- Contains database models (JPA, MongoDB, etc.), different from domain models.

### 📂 `dataprovider/repository/jpa`
- Contains repositories that use JPA, Hibernate, or other ORMs.

### 📂 `dataprovider/repository/custom`
- Custom query implementations.

### 📂 `dataprovider/mapper`
- Maps between database entities and domain models.

### 📂 `dataprovider/gateway`
- Implementations of the `core/gateway` interfaces, using the repository to store and retrieve data.

### 📂 `dataprovider/rest`
- Consumes external APIs.

### 📂 `dataprovider/rest/client`
- Implementations of HTTP calls (RestTemplate, Feign).

### 📂 `dataprovider/rest/dto`
- Models used to send/receive data from external APIs.

### 📂 `dataprovider/rest/mapper`
- Maps between external DTOs and domain models.

### 📂 `dataprovider/messaging`
- Publishing and consuming asynchronous messages (Kafka, RabbitMQ).

### 📂 `dataprovider/messaging/kafka/consumer`
- Logic to consume messages from Kafka.

### 📂 `dataprovider/messaging/kafka/producer`
- Producing messages.

### 📂 `dataprovider/messaging/kafka/config`
- Kafka configurations.

---

## 3. Entrypoint (Communication Interface)

Layer responsible for interacting with external clients (REST APIs, CLI, etc.).  

### 📂 `entrypoint/controller`
- Exposes REST endpoints using Spring Web.

### 📂 `entrypoint/dto`
- DTOs used for input and output of data in endpoints.

### 📂 `entrypoint/mapper`
- Converts DTOs into domain models.

---

## 4. Config (General Configuration)

### 📂 `config`
- Global project configurations (Beans, Security, etc.).

---

## 🔄 **Data Flow**
1️⃣ **Client sends a request to `GET /users/{id}`**  
2️⃣ **Controller receives the request and calls the Use Case**  
3️⃣ **Use Case calls the Gateway interface**  
4️⃣ **Gateway calls the Repository**  
5️⃣ **Repository fetches data from the database**  
6️⃣ **Entity is mapped to Domain Model**  
7️⃣ **Use Case returns the User Domain Model**  
8️⃣ **Controller maps Domain Model to DTO**  
9️⃣ **Response is returned to the client**  

---

## 📂 **Code Implementation**

### **1️⃣ Domain Model (`core/domain/User.java`)**
```java
public class User {
    private Long id;
    private String name;
    private String email;

    public User(Long id, String name, String email) {
        this.id = id;
        this.name = name;
        this.email = email;
    }
}
```

### **2️⃣ Gateway Interface (`core/gateway/UserGateway.java`)**
```java
public interface UserGateway {
    Optional<User> findById(Long id);
}
```

### **3️⃣ Use Case (`core/usecase/FindUserByIdUseCase.java`)**
```java
public class FindUserByIdUseCase {
    private final UserGateway userGateway;

    public FindUserByIdUseCase(UserGateway userGateway) {
        this.userGateway = userGateway;
    }

    public Optional<User> execute(Long id) {
        return userGateway.findById(id);
    }
}
```

### **4️⃣ Entity (`dataprovider/repository/entity/UserEntity.java`)**
```java
@Entity
@Table(name = "users")
public class UserEntity {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
    private String email;
}
```

### **5️⃣ Repository (`dataprovider/repository/jpa/UserJpaRepository.java`)**
```java
public interface UserJpaRepository extends JpaRepository<UserEntity, Long> {}
```

### **6️⃣ Mapper (`dataprovider/mapper/UserMapper.java`)**
```java
public class UserMapper {
    public static User toDomain(UserEntity entity) {
        return new User(entity.getId(), entity.getName(), entity.getEmail());
    }
}
```

### **7️⃣ Gateway Implementation (`dataprovider/gateway/UserGatewayImpl.java`)**
```java
@Component
public class UserGatewayImpl implements UserGateway {
    private final UserJpaRepository userJpaRepository;

    public UserGatewayImpl(UserJpaRepository userJpaRepository) {
        this.userJpaRepository = userJpaRepository;
    }

    @Override
    public Optional<User> findById(Long id) {
        return userJpaRepository.findById(id).map(UserMapper::toDomain);
    }
}
```

### **8️⃣ DTO (`entrypoint/dto/UserResponse.java`)**
```java
public class UserResponse {
    private Long id;
    private String name;
    private String email;
}
```

### **9️⃣ DTO Mapper (`entrypoint/mapper/UserResponseMapper.java`)**
```java
public class UserResponseMapper {
    public static UserResponse toResponse(User user) {
        return new UserResponse(user.getId(), user.getName(), user.getEmail());
    }
}
```

### **🔟 Controller (`entrypoint/controller/UserController.java`)**
```java
@RestController
@RequestMapping("/users")
public class UserController {
    private final FindUserByIdUseCase findUserByIdUseCase;

    public UserController(FindUserByIdUseCase findUserByIdUseCase) {
        this.findUserByIdUseCase = findUserByIdUseCase;
    }

    @GetMapping("/{id}")
    public ResponseEntity<UserResponse> findById(@PathVariable Long id) {
        return findUserByIdUseCase.execute(id)
                .map(user -> ResponseEntity.ok(UserResponseMapper.toResponse(user)))
                .orElse(ResponseEntity.notFound().build());
    }
}
```

---

## 📌 Flow Summary

1️⃣ The client calls `GET /users/{id}`.
2️⃣ The Controller (`UserController`) receives the request.  
3️⃣ It calls `FindUserByIdUseCase`, passing the id.  
4️⃣ The Use Case calls `UserGateway.findById(id)`.  
5️⃣ The Gateway (UserGatewayImpl) queries the `UserJpaRepository`.  
6️⃣ The Repository searches the database and returns the `UserEntity`.  
7️⃣ The Mapper (UserMapper) converts `UserEntity → User`.  
8️⃣ The Use Case returns the `User` to the **Controller**.  
9️⃣ The Controller maps the `User` to `UserResponse`.  
🔟 The result is sent as a response to the client.

---

## ✅ **Advantages of this Architecture**
- **Separation of Concerns:** Domain logic is independent of frameworks and infrastructure.
- **Testability:** Components can be unit tested independently.
- **Scalability:** Easy to extend without breaking existing functionality.
- **Maintainability:** Code is organized and structured.

---