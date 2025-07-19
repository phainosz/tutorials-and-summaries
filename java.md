# Anotações gerais sobre Java

- [Introdução](#introdução)
- [Instalação](#instalação)
- [Geral](#geral)
- [Comandos](#comandos)
- [Condições IF e Switch](#condições-if-e-switch)
- [Arrays](#arrays)
- [Loops](#loops)
- [Funções (Métodos)](#funções-métodos)
- [Enums](#enums)
- [Null Safety](#null-safety)
- [Classes](#classes)
- [Interfaces](#interfaces)
- [Tratamento de Erros](#tratamento-de-erros)
- [Generics](#generics)
- [Lambdas](#lambdas)
- [Programação Orientada a Objetos](#programação-orientada-a-objetos)
- [Princípios SOLID](#princípios-solid)
- [Threads e Concorrência](#threads-e-concorrência)
- [Gerenciamento de Memória](#gerenciamento-de-memória)
- [Gradle](#gradle)

## Introdução

- **Java** é uma linguagem de programação orientada a objetos, multiplataforma, robusta e amplamente utilizada, mantida pela Oracle. Criada em 1995 pela Sun Microsystems, ela é usada em diversas áreas.
- Muito usada em back-end, aplicações Android, sistemas corporativos, aplicações desktop e embarcadas.
- Por que usar Java?
  - **Portabilidade**: Funciona em qualquer sistema operacional com JVM.
  - **Ecossistema**: Frameworks como Spring, Hibernate e Micronaut.
  - **Tipagem forte**: Reduz erros em tempo de execução.
  - **Comunidade**: Amplo suporte e vasta quantidade de bibliotecas.
  - **Estabilidade**: Linguagem madura, usada em sistemas críticos.

## Instalação

- Para instalar o **Java**, é recomendado usar o [sdkman](https://sdkman.io/) ou baixar o JDK diretamente do site da [Oracle](https://www.oracle.com/java/technologies/downloads/).
- O sdkman é um gerenciador de versões para linguagens e ferramentas como Java, Maven, Gradle, entre outros.
- Para instalar o sdkman e Java, execute:

```
curl -s "https://get.sdkman.io" | bash
source "$HOME/.sdkman/bin/sdkman-init.sh"
sdk install java
java -version
javac -version
```

## Geral

- **JVM**, java virtual machine, é uma especificação que provê um ambiente de execução(runtime environment) para
  executar **bytecode** e converte para código de máquina.
- **JRE**, java runtime environment, é uma combinação de ferramentas usadas para desenvolver aplicações java. É a
  implementação da **JVM**. **JRE** não é usado para desenvolvimento e sim para executar código java compilado.
- **JDK**, java development kit, provê as ferramentas para debugar, compilar e executar um programa. Contém todo o
  ferramental que o **JRE** fornece.
- **Variáveis** são containers para guardar valores para determinados tipos. Ao criar uma *variável*, damos um nome,
  tipo e valor para ela.
  - Em **java** podemos criar variáveis **primitivas** ou **não-primitivas**
  - **Primitivos**: Tipos básicos que armazenam valores diretamente.
    | Tipo      | Descrição                          | Tamanho         | Exemplo         |
    |-----------|------------------------------------|-----------------|-----------------|
    | `boolean` | Verdadeiro ou falso                | 1 bit           | `true`, `false` |
    | `char`    | Caractere Unicode                  | 16 bits         | `'A'`           |
    | `byte`    | Inteiro de 8 bits                  | 8 bits          | `127`           |
    | `short`   | Inteiro de 16 bits                 | 16 bits         | `32767`         |
    | `int`     | Inteiro de 32 bits                 | 32 bits         | `2147483647`    |
    | `long`    | Inteiro de 64 bits                 | 64 bits         | `9223372036854775807` |
    | `float`   | Ponto flutuante de 32 bits         | 32 bits         | `3.14f`         |
    | `double`  | Ponto flutuante de 64 bits         | 64 bits         | `3.14`          |

- **Não-Primitivos**: Referências a objetos, como classes, interfaces e arrays.
  - Exemplo: `String`, `Integer`, `ArrayList`.
- **Java** possui muitas palavras-chaves(keywords) que foram criadas com um propósito específico e usadas dentro do
  código, alguns exemplos:
  - `class`: Define uma classe.
  - `public`: Modificador de acesso, permite acesso de qualquer lugar.
  - `static`: Indica que um método ou atributo pertence à classe, não a instâncias.
  - `void`: Indica que um método não retorna valor.
  - `main`: Ponto de entrada de uma aplicação Java.
- Modificadores de acesso em **java**, servem alterar a acessibilidade ou escopo de: *classe*, *método*, *atributos* e
  *construtores*.
  - `public`: Acessível de qualquer lugar.
  - `private`: Acessível somente dentro da classe.
  - `protected`: Acessível na classe, subclasses e mesmo pacote.
  - `package-private` (sem modificador): Acessível dentro do mesmo pacote.
- Exemplo básico:

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, world!"); // Print to console
    }
}
```

## Comandos

- Para compilar um arquivo `.java`:

```
javac HelloWorld.java
```

- Para executar o programa compilado:

```
java HelloWorld
```

- Para gerar um arquivo JAR executável:

```
jar cfe app.jar HelloWorld *.class
java -jar app.jar
```

## Condições IF e Switch

- **If-Else**:

```java
int age = 20;
if (age < 18) {
    System.out.println("Minor"); // Print if under 18
} else if (age >= 18 && age < 60) {
    System.out.println("Adult"); // Print if between 18 and 59
} else {
    System.out.println("Senior"); // Print if 60 or older
}
```

- **Switch** (suporta `int`, `String`, `enum`, etc., e `switch` expression desde Java 14):

```java
String day = "MONDAY";
switch (day) {
    case "MONDAY":
        System.out.println("Start of the week"); // Print for Monday
        break;
    case "FRIDAY":
        System.out.println("Weekend approaching"); // Print for Friday
        break;
    default:
        System.out.println("Another day"); // Print for other days
}
```

- **Switch Expression** (Java 14+):

```java
String result = switch (day) {
    case "MONDAY" -> "Start of the week"; // Return for Monday
    case "FRIDAY" -> "Weekend approaching"; // Return for Friday
    default -> "Another day"; // Return for other days
};
```

## Arrays

- Declaração e inicialização:

```java
int[] numbers = new int[5]; // Array size 5
int[] initialized = {1, 2, 3, 4, 5}; // Starting values
```

- Acesso e manipulação:

```java
numbers[0] = 10; // Set value
System.out.println(numbers[0]); // Access value
System.out.println(Arrays.toString(numbers)); // Print array
```

- Array multidimensional:

```java
int[][] matrix = {{1, 2}, {3, 4}}; // 2D array
```

- Utilitários da classe `Arrays` (pacote `java.util`):
  - `Arrays.sort(numbers);` // Ordena o array
  - `Arrays.fill(numbers, 0);` // Preenche com valor
  - `Arrays.copyOf(numbers, newLength);` // Cria cópia com novo tamanho

```java
import java.util.Arrays;
int[] numbers = {5, 2, 8, 1};
Arrays.sort(numbers); // Sort array
System.out.println(Arrays.toString(numbers)); // Print [1, 2, 5, 8]
```

- Cuidados:
  - Evite acessar índices fora dos limites do array (causa `ArrayIndexOutOfBoundsException`).
  - Arrays têm tamanho fixo, para tamanhos dinâmicos, use `ArrayList`.

## Loops

- Em programação, **loops** são usados para repetir um bloco de código enquanto uma condição for verdadeira ou enquanto houverem elementos a serem percorridos.

- **For**:

```java
for (int i = 0; i < 10; i++) {
    System.out.println(i); // Print index
}
```

- **For-Each** (para coleções e arrays):

```java
int[] numbers = {1, 2, 3};
for (int num : numbers) {
    System.out.println(num); // Print each number
}
```

- **While**:

```java
int i = 0;
while (i < 10) {
    System.out.println(i); // Print index
    i++;
}
```

- **Do-While**:

```java
int j = 0;
do {
    System.out.println(j); // Print index
    j++;
} while (j < 10);
```

- **Break e Continue**:

```java
for (int i = 0; i < 10; i++) {
    if (i == 5) {
        break; // Stop loop at 5
    }
    System.out.println(i); // Print index
}
for (int j = 0; j < 10; j++) {
    if (j == 5) {
        continue; // Skip iteration at 5
    }
    System.out.println(j); // Print index
}
```

## Funções (Métodos)

- Funções são blocos de código reutilizáveis que executam uma tarefa específica.

- Declaração de método:

```java
public int sum(int a, int b) {
    return a + b; // Return sum
}

System.out.println(sum(2, 3)); // Print 5
```

- Método com parâmetros variáveis (varargs):

```java
public int sumAll(int... numbers) {
    int total = 0;
    for (int num : numbers) {
        total += num; // Add each number
    }
    return total; // Return total
}

System.out.println(sumAll(1, 2, 3, 4)); // Print 10
```

## Enums

- Enums são usados para representar um conjunto fixo de constantes.

```java
enum Day {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY
}

Day today = Day.MONDAY;
if (today == Day.MONDAY) {
    System.out.println("It's Monday!"); // Print message
}
```

- Enum com atributos:

```java
enum Status {
    ACTIVE(1), INACTIVE(0);
    private final int code;
    Status(int code) { this.code = code; } // Constructor
    public int getCode() { return code; } // Get code
}
```

## Null Safety

- Java não possui null safety nativa como Kotlin, mas pode-se usar `Optional` (Java 8+):

```java
import java.util.Optional;

Optional<String> name = Optional.ofNullable(null);
System.out.println(name.orElse("Default")); // Print default value
```

- Verificação manual:

```java
String value = null;
if (value != null) {
    System.out.println(value.length()); // Print length
} else {
    System.out.println("Null value"); // Print null message
}
```

## Classes

- Classes são a base da programação orientada a objetos.
- Elas podem conter atributos (propriedades) e métodos (funções).

```java
public class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name; // Set name
        this.age = age; // Set age
    }

    public String getName() { return name; } // Get name
    public void setName(String name) { this.name = name; } // Set name
}
```

- Instanciação:

```java
Person person = new Person("Alice", 30);
System.out.println(person.getName()); // Print Alice
```

## Interfaces

- Interfaces são contratos que definem **métodos e propriedades** que uma classe pode implementar.

```java
public interface Animal {
    void makeSound(); // Abstract method
}

public class Dog implements Animal {
    @Override
    public void makeSound() {
        System.out.println("Woof!"); // Dog sound
    }
}

Animal dog = new Dog();
dog.makeSound(); // Print Woof!
```

## Tratamento de Erros

- Tratamento de erros baseado em exceções.
- O uso de `try`, `catch`, `finally` permite capturar e lidar com exceções em tempo de execução.

- Bloco try-catch:

```java
try {
    int result = 10 / 0; // Attempt division
} catch (ArithmeticException e) {
    System.out.println("Division by zero!"); // Handle error
} finally {
    System.out.println("Always executes"); // Final block
}
```

- Lançamento de exceção:

```java
public void checkAge(int age) throws IllegalArgumentException {
    if (age < 18) {
        throw new IllegalArgumentException("Invalid age"); // Throw exception
    }
}
```

- Tipos de Exceções:
  - **Checked**: Devem ser tratadas ou declaradas (e.g., `IOException`).
  - **Unchecked**: Não precisam ser tratadas (e.g., `RuntimeException`, `NullPointerException`).

## Generics

- Generics permitem criar classes, interfaces e métodos que podem trabalhar com diferentes tipos de dados, especificando o tipo desejado no momento da utilização. Em vez de trabalhar com tipos concretos, como Integer ou String, você pode usar placeholders ou outros caracteres para representar tipos genéricos.
- Placeholders mais usados em Java:
  - `T` Representa um tipo geral, utilizado quando não há necessidade de uma restrição específica sobre o tipo. `Box<T>`.
  - `E` Usado para representar elementos de coleções, como listas ou arrays. `List<E>`.
  - `K, V` Usados em mapas para representar chave(key) e valor(value). `Map<K, V>`
  - `R` Usado para indicar resultado ou retorno. `Function<T, R>`.
  - `U, S` Auxiliares usados quando existe mais de um tipo envolvido. `BiFunction<T, U, R>`.

```java
class Box<T> {
    private T content;

    public void setContent(T content) { this.content = content; }
    public T getContent() { return content; }
}

Box<String> box = new Box<>();
box.setContent("Text");
System.out.println(box.getContent()); // Print: Text
```

- Generics não funcionam com tipos primitivos (como int, char, etc.). Então, você deve usar suas classes wrapper (Integer, Character, etc.).
- Podemos criar apenas métodos genéricos sem que a classe precise fazer o uso de generics:

```java
class Helper {
    public static <T> void changeContent(Box<T> first, Box<T> second) {
        T temp = first.getContent();
        first.setContent(second.getContent());
        second.setContent(temp);
    }
}
```

## Lambdas

- São uma forma concisa de representar funções anônimas.
- Não necessitam de nome, classe ou precisam ser declaradas.
- Introduzida no Java 8, permitem implementar de forma curta as interfaces funcionais(`Consumer`, `Predicate`, `Supplier`, `Function`, etc).
  - As principais interfaces funcionais se encontram no pacote `java.util.funtion` do java.
- Uma interface funcional possui apenas um método abstrato.

```java
@FunctionalInterface
interface Operation {
  int execute(int a, int b);
}

Operation sumOperation = (a, b) -> a + b;
sumOperation.execute(1, 2);
```

## Programação Orientada a Objetos

- A Programação Orientada a Objetos (OOP) é um paradigma onde o código é organizado em **classes** e **objetos**, modelando entidades do mundo real.
- **Programação Orientada a Objetos (OOP)** organiza o código em objetos que representam entidades do mundo real com atributos (estado) e métodos (comportamento).
- Java é totalmente orientado a objetos e fornece suporte completo a:
    - Classes
    - Objetos
    - Herança
    - Encapsulamento
    - Polimorfismo
    - Abstração
- Esses pilares tornam o código mais modular, manutenível e reutilizável.

### Classes e Objetos

- Uma **classe** é uma estrutura que define **propriedades** (variáveis) e **comportamentos** (funções).
- Ela funciona como um **molde** para criar objetos.

```java
// This class defines a Person with a name and age
class Person {
  private final String name;
  private final int age;

  public Person(String name, int age) {
    this.name = name;
    this.age = age;
  }

  public void introduce() {
    System.out.printf("Hi, my name is %s and I am %d years old!", this.name, this.age);
  }
}
```

- Um objeto é uma instância concreta de uma classe.
  Quando você instancia uma classe, cria um objeto com seus próprios dados.

```java
public static void main(String[] args) {
    Person person = new Person("John", 30);
    person.introduce();
}
```

### Encapsulamento

- Encapsulamento oculta os detalhes internos de uma classe, permitindo acesso somente através de métodos públicos.
- Isso protege os dados e mantém o controle sobre seu uso.

```java
public class User {
    private String name;
    private int age;

    public String getName() { return name; } // Get name
    public void setName(String name) {
        if (name != null && !name.isEmpty()) {
            this.name = name; // Set name if valid
        }
    }

    public int getAge() { return age; } // Get age
    public void setAge(int age) {
        if (age > 0) {
            this.age = age; // Set age if valid
        }
    }
}
  ```

### Herança

- Permite que uma classe herde atributos e métodos de outra, promovendo reuso e polimorfismo.

```java
public class Animal {
    protected String name;

    public void move() {
        System.out.println("The animal moves"); // Generic movement
    }
}

public class Dog extends Animal {
    public Dog(String name) {
        this.name = name; // Set name
    }

    public void bark() {
        System.out.println("The dog barks"); // Dog-specific behavior
    }
}

Dog dog = new Dog("Rex");
dog.move(); // Inherited behavior
dog.bark(); // Dog-specific behavior
```

### Polimorfismo

- Permite que objetos de diferentes tipos respondam de forma diferente a uma mesma chamada de método.

- **Overloading**, métodos com o mesmo nome, mas parâmetros diferentes:

```java
public class Calculator {
    public int add(int a, int b) {
        return a + b; // Add two integers
    }

    public int add(int a, int b, int c) {
        return a + b + c; // Add three integers
    }

    public double add(double a, double b) {
        return a + b; // Add two doubles
    }
}

Calculator calc = new Calculator();
System.out.println(calc.add(5, 10)); // Print 15
System.out.println(calc.add(5, 10, 15)); // Print 30
System.out.println(calc.add(5.5, 10.5)); // Print 16.0
```

- **Overriding**, subclasses redefinem métodos da superclasse:

```java
public class Animal {
    public void sound() {
        System.out.println("Some generic animal sound"); // Generic sound
    }
}

public class Dog extends Animal {
    @Override
    public void sound() {
        System.out.println("Bark"); // Dog-specific sound
    }
}

Animal animal = new Dog();
animal.sound(); // Print Bark
    ```

### Abstração

- Abstração foca apenas nos detalhes essenciais, ocultando a complexidade desnecessária.
- A abstração permite que classes concretas implementem apenas o que for necessário, escondendo detalhes da
  implementação.
- Pode ser feita com interfaces ou classes abstratas.

```java
public interface Database {
    void connect(); // Abstract method
}

public class MySQLDatabase implements Database {
    @Override
    public void connect() {
        System.out.println("Connecting to MySQL database..."); // MySQL connection
    }
}

Database db = new MySQLDatabase();
db.connect(); // Print MySQL connection message
```

## Princípios SOLID

- O SOLID é um conjunto de **cinco princípios** da programação orientada a objetos que ajudam a tornar o código mais *
  *modular**, **flexível** e **fácil de manter**.
- Esses princípios são:
    - **S** - Single Responsibility Principle (Princípio da Responsabilidade Única)
    - **O** - Open/Closed Principle (Princípio Aberto/Fechado)
    - **L** - Liskov Substitution Principle (Princípio da Substituição de Liskov)
    - **I** - Interface Segregation Principle (Princípio da Segregação de Interfaces)
    - **D** - Dependency Inversion Principle (Princípio da Inversão de Dependência)

### S — Single Responsibility Principle (Responsabilidade Única)

- Cada classe deve ter **uma única responsabilidade** e **um único motivo para mudar**.
- Separar responsabilidades facilita testes, manutenção e reaproveitamento de código.

  ```java
  // Bad: Multiple responsibilities
  public class UserManager {
      public void saveUser(String user) {
          System.out.println("Saving user"); // Save user
      }

      public void sendWelcomeEmail(String email) {
          System.out.println("Sending email"); // Send email
      }
  }

  // Good: Single responsibility
  public class UserManager {
      public void saveUser(String user) {
          System.out.println("Saving user"); // Save user
      }
  }

  public class EmailService {
      public void sendWelcomeEmail(String email) {
          System.out.println("Sending email"); // Send email
      }
  }
  ```

### O — Open/Closed Principle (Aberto para extensão, fechado para modificação)

- Você deve poder adicionar comportamentos sem modificar o código existente.

  ```java
  public interface Operation {
      int execute(int a, int b); // Execute operation
  }

  public class SumOperation implements Operation {
      public int execute(int a, int b) {
          return a + b; // Add numbers
      }
  }

  public class MultiplyOperation implements Operation {
      public int execute(int a, int b) {
          return a * b; // Multiply numbers
      }
  }
  ```

### L — Liskov Substitution Principle (Substituição de Liskov)

- Subclasses devem ser substituíveis por suas superclasses sem alterar o comportamento.

```java
  // Bad: Square breaks Rectangle behavior
  public class Rectangle {
      protected int width, height;

      public void setWidth(int width) { this.width = width; } // Set width
      public void setHeight(int height) { this.height = height; } // Set height
      public int getArea() { return width * height; } // Calculate area
  }

  public class Square extends Rectangle {
      @Override
      public void setWidth(int width) {
          this.width = width;
          this.height = width; // Breaks expected behavior
      }
  }

  // Good: Separate classes
  public class Rectangle {
      protected int width, height;

      public void setDimensions(int width, int height) {
          this.width = width; // Set width
          this.height = height; // Set height
      }

      public int getArea() { return width * height; } // Calculate area
  }

  public class Square {
      private int side;

      public void setSide(int side) { this.side = side; } // Set side
      public int getArea() { return side * side; } // Calculate area
  }
  ```

### I — Interface Segregation Principle (Segregação de Interfaces)

- Classes não devem ser forçadas a implementar métodos desnecessários.
- Interfaces pequenas e específicas respeitam a coesão e facilitam a manutenção.

  ```java
  // Good: Segregated interfaces
  public interface Bird {
      void eat(); // Common behavior
  }

  public interface FlyingBird {
      void fly(); // Flying behavior
  }

  public interface SwimmingBird {
      void swim(); // Swimming behavior
  }

  public class Penguin implements Bird, SwimmingBird {
      public void eat() {
          System.out.println("Penguin eating"); // Eat behavior
      }

      public void swim() {
          System.out.println("Penguin swimming"); // Swim behavior
      }
  }
  ```

### D — Dependency Inversion Principle (Inversão de Dependência)

- Dependa de **abstrações**, não de implementações concretas.

  ```java
  public interface DataStorage {
      void save(String data); // Save data
  }

  public class Database implements DataStorage {
      public void save(String data) {
          System.out.println("Saving to database"); // Database save
      }
  }

  public class UserService {
      private DataStorage dataStorage;

      public UserService(DataStorage dataStorage) {
          this.dataStorage = dataStorage; // Inject dependency
      }

      public void saveUser(String user) {
          dataStorage.save(user); // Use abstraction
      }
  }
  ```

## Threads e Concorrência

- Java suporta programação concorrente com threads.

```java
public class MyThread extends Thread {
    @Override
    public void run() {
        System.out.println("Thread running"); // Thread action
    }
}
MyThread thread = new MyThread();
thread.start(); // Start thread
```

- `ExecutorService` gerencia um pool de threads:

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

ExecutorService executor = Executors.newFixedThreadPool(2);
executor.submit(() -> System.out.println("Async task")); // Submit task
executor.shutdown(); // Shutdown executor
```

## Gerenciamento de Memória

- Java usa um **Garbage Collector (GC)** para liberar memória automaticamente.

- **Heap**: Armazena objetos.
- **Stack**: Armazena variáveis locais e chamadas de métodos.
- **GC**: Remove objetos não referenciados.

## Gradle

- Gradle é uma ferramenta de automação de builds moderna, amplamente usada em projetos Java, Android, etc.
- Configuração básica (`build.gradle`):

```groovy
plugins {
    id 'java'
}
repositories {
    mavenCentral()
}
dependencies {
    implementation 'org.springframework.boot:spring-boot-starter:3.2.0'
}
```

- Comandos úteis:
```bash
./gradlew build    # Compile and run tests
./gradlew run      # Run application
./gradlew clean    # Clean build
```