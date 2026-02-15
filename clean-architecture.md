# Clean Architecture - Exemplo

## Visão Geral
Este documento explica o fluxo de dados em um projeto baseado em Clean Architecture, implementando um caso de uso simples: **Buscar Usuário por ID.**

O objetivo é demonstrar claramente as responsabilidades de cada camada, respeitando os princípios de independência de framework, separação de responsabilidades e inversão de dependência.

### Estrutura de Pastas
```
src/main/java/com/example/cleanarchitecture
├── core
│   ├── domain
│   ├── usecase
│   ├── exception
│   └── gateway
├── dataprovider
│   ├── database
│   │   ├── config
│   │   ├── entity
│   │   ├── mapper
│   │   └── repository
│   ├── integration
│   │   ├── config
│   │   ├── client
│   │   ├── dto
│   │   └── mapper
│   ├── integration
│   │   ├── kafka
│   │   │   ├── config
│   │   │   ├── consumer
│   │   │   └── config
├── entrypoint
│   ├── controller
│   │   ├── config
│   │   ├── dto
│   │   └── mapper
│   ├── worker
│   │   ├── config
│   │   ├── dto
│   │   └── mapper
└── config
```

## Camadas e Responsabilidades

### 1. Core (Regras de Negócio)

A camada **core** contém o coração da aplicação. Aqui ficam as regras de negócio puras, sem dependência de frameworks, banco de dados ou detalhes de infraestrutura.

#### `core/domain`

- Contém as entidades de domínio.
- Representa conceitos essenciais do negócio.
- Classes simples (POJOs), sem anotações de framework.

#### `core/usecase`

- Contém os casos de uso (Application Business Rules).
- Orquestra o fluxo entre domínio e gateways.
- Depende apenas de interfaces, nunca de implementações.

#### `core/exception`

- Exceções de domínio.
- Representam erros de regra de negócio.
- Exemplo: `UserNotFoundException`.

#### `core/gateway`

- Define contratos (interfaces) para acesso a recursos externos.
- Exemplo: banco de dados, APIs externas, mensageria.

---

### 2. Data Provider (Implementações de Infraestrutura)

Responsável por implementar os *gateways* definidos no **core**. Aqui ficam os detalhes técnicos e dependências externas.

#### `dataprovider/database`

- Camada de persistência de dados.

#### `dataprovider/integration`

- Integração com APIs externas.

#### `dataprovider/broker`

- Comunicação de saída assíncrona.

---

### 3. Entrypoint (Interface de Entrada)

#### `entrypoint/controller`

- Entrada através de APIs.

#### `entrypoint/worker`

- Consumidores de mensageria assíncrona.

---

## Exemplo buscar usuário por ID

### Fluxo de Dados

- Cliente chama `GET /users/{id}`
- Controller recebe a requisição
- Controller chama o Use Case
- Use Case chama o Gateway
- Gateway acessa o Repository
- Dados do banco são convertidos para Domínio
- Use Case retorna o domínio
- Controller converte para DTO de resposta
- Resposta é enviada ao cliente

---

### Código

#### Domain Model (`core/domain/User.java`)

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

#### Gateway Interface (`core/gateway/UserGateway.java`)

```java
public interface UserGateway {
    Optional<User> findById(Long id);
}
```

#### Use Case (`core/usecase/FindUserByIdUseCase.java`)

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

#### Entity (`dataprovider/repository/entity/UserEntity.java`)

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

#### Repository (`dataprovider/repository/jpa/UserJpaRepository.java`)

```java
public interface UserJpaRepository extends JpaRepository<UserEntity, Long> {}
```

#### Mapper (`dataprovider/mapper/UserMapper.java`)

```java
public class UserMapper {
    public static User toDomain(UserEntity entity) {
        return new User(entity.getId(), entity.getName(), entity.getEmail());
    }
}
```

#### Gateway Implementation (`dataprovider/gateway/UserGatewayImpl.java`)

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

#### DTO (`entrypoint/dto/UserResponse.java`)

```java
public class UserResponse {
    private Long id;
    private String name;
    private String email;
}
```

#### DTO Mapper (`entrypoint/mapper/UserResponseMapper.java`)

```java
public class UserResponseMapper {
    public static UserResponse toResponse(User user) {
        return new UserResponse(user.getId(), user.getName(), user.getEmail());
    }
}
```

#### Controller (`entrypoint/controller/UserController.java`)

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

## Benefícios da Clean Architecture

- Baixo acoplamento entre regras de negócio e infraestrutura
- Alta testabilidade (use cases sem Spring)
- Facilidade de manutenção e evolução
- Flexibilidade para trocar frameworks sem impacto no core