# Anotaçẽs gerais sobre Kotlin

- [Introdução](#introdução)
- [Instalação](#instalação)
- [Geral](#geral)
- [Comandos](#comandos)
- [Condições IFs e Switch](#condições-ifs-e-when)
- [Arrays](#arrays)
- [Loops](#loops)
- [Funções](#funções)
- [Enums](#enums)
- [Null Safety](#null-safety)
- [Classes](#classes)
- [Intefaces](#interfaces)
- [Tratamento de Erros](#tratamento-de-erros)
- [Programação Orientada a Objetos](#programação-orientada-a-objetos)
- [SOLID](#solid)
- [Corroutines](#corroutines)
- [Gradle](#gradle)

## Introdução

- **Kotlin** é uma linguagem moderna, desenvolvida pela JetBrains, totalmente interoperável com Java, concisa e segura.
  É usada para back-end, Android, e até front-end com Kotlin/JS.
- Por que usar Kotlin no back-end?
    - Totalmente compatível com o ecossistema Java (Spring Boot, Kafka, etc.)
    - Null safety nativa.
    - Código mais conciso e expressivo.
    - Corrotinas para facilitar concorrência e IO assíncrono.

## Instalação

- Para instalar o **Kotlin** podemos fazer a instalaćão através do *sdkman*.
- [sdkman](https://sdkman.io/), serve para **Kotlin** e outras ferramentas.
- Instalar o *sdkman* e após isso rodar o comando `sdk install kotlin`.

## Geral

- Kotlin é uma linguagem de programação moderna, concisa, segura e fortemente tipada.
- Suporta os paradigmas Orientado a Objetos e funcional.
- Kotlin roda sobre a JVM, o que significa que é multiplataforma, pode ser usado para criar aplicações backend, Android,
  desktop, web e até rodar em JavaScript ou código nativo (via Kotlin/Native).
- Quando compilamos um programa Kotlin, o compilador converte o código .kt para bytecode, que é executado pela JVM.
- JVM (Java Virtual Machine) é uma especificação que fornece um ambiente de execução para código Java/Kotlin compilado.
- JRE (Java Runtime Environment) é a implementação da JVM, usada para executar código.
- JDK (Java Development Kit) fornece ferramentas para compilar, debugar e executar o código, necessário para o
  desenvolvimento com Kotlin na JVM.
- Variáveis em Kotlin também são containers para armazenar valores de tipos específicos:
    - Declaradas com val (imutável) ou var (mutável).
    - Kotlin infere o tipo automaticamente, mas também permite declaração explícita:
        ```kotlin
        val name = "Fulano"
        var age: Int = 21
        ```
- Modificadores de acesso em Kotlin funcionam de forma parecida com Java:
    - `private`: visível apenas na classe, arquivo ou escopo onde foi definido.
    - `public`: visível em todos os lugares (padrão).
    - `protected`: visível na classe e subclasses.
    - `internal`: visível apenas dentro do mesmo módulo (um diferencial de Kotlin em relação ao Java).

## Comandos

- Para compilar um arquivo `.kt`, podemos usar o comando `kotlinc`.
    - Ex:
        ```
        kotlinc Hello.kt -include-runtime -d Hello.jar
        ```
    - Isso irá compilar o arquivo e gerar um executável `.jar` com o bytecode.
    - A flag `-include-runtime` inclui a runtime do Kotlin no `.jar`.
    - Para executar o arquivo `.jar` precisamos do **Java** instalado. É executado com `java -jar Hello.jar`.
- Também é possível compilar apenas para `.class`, sem gerar `.jar` com `kotlinc Hello.kt`.
    - Isso criará um `HelloKt.class`, nome do arquivo + Kt.
- Podemos executar diretamente, sem compilar, usando o interpretador, `kotlinc -script Hello.kts`.
    - Arquivos com extensão `.kts` (Kotlin Script) são usados para **scripts rápidos**, como automações simples,
      configurações ou tarefas pequenas, sem a necessidade de `fun main`.

## Condições IFs e When

- Usados para controle condicional usando uma *variável* ou valor específico como base.
    - Exemplo com `if`:
        ```kotlin
        val age = 20

        if (age < 18) {
          println("Menor de idade")
        } else if (age in 18..59) {
          println("Adulto")
        } else {
          println("Idoso")
        }
        ```
- Em Kotlin, usamos `when` no lugar do `switch`.
    - Ex:
        ```kotlin
        val number = 0

        when (number) {
          0 -> println("0")
          1 -> println("1")
          2 -> println("2")
          else -> println("error")
        }
        ```
- Também podemos usar when como expressão, retornando um valor.
    - Ex:
        ```kotlin
        val day = 4

        val result = when (day) {
          in 0..3 -> "low"
          in 4..6 -> "medium"
          in 7..9 -> "high"
          else -> "error"
        }

        println(result)
        ```

## Arrays

- **Arrays** são estruturas de dados lineares que armazenam múltiplos valores do mesmo tipo em posições contíguas de
  memória.
- Em Kotlin, arrays são indexados a partir do índice **0**, assim como em Java.
- O acesso aos elementos é feito pelo índice, e o tamanho do array é fixo após a criação.

### Criação de arrays

- Criando array vazio com tamanho fixo:
    ```kotlin
    val array = Array<Int>(2) { 0 }
    array[0] = 1
    array[1] = 2
    ```

- Inicialização com valores:
    ```kotlin
    val array2 = arrayOf(1, 2, 3, 4, 5)
    ```

- Criando arrays de tipos primitivos:
    ```kotlin
    val intArray = intArrayOf(1, 2, 3)
    val doubleArray = doubleArrayOf(1.1, 2.2, 3.3)
    val charArray = charArrayOf('a', 'b', 'c')
    ```

### Acessando elementos

- Podemos acessar os valores por índice:
    ```kotlin
    println(array2[0]) // imprime 1
    println(array2[1]) // imprime 2
    ```

- Também podemos modificar:
    ```kotlin
    array2[0] = 10
    ```

### Iterando sobre arrays

- Usando `for`:
    ```kotlin
    for (element in array2) {
      println(element)
    }
    ```

- Usando índices:
    ```kotlin
    for (i in array2.indices) {
      println("Index $i -> ${array2[i]}")
    }
    ```

- Usando `withIndex()`:
    ```kotlin
    for ((index, value) in array2.withIndex()) {
      println("[$index] = $value")
    }
    ```

### Tamanho do array

- Podemos obter o tamanho com `.size`:
    ```kotlin
    println(array2.size)
    ```

### Observações

- `Array<T>` é uma classe genérica, usada para tipos de referência.
- Para melhor performance com tipos primitivos (`Int`, `Double`, `Boolean`, etc), use `intArrayOf`, `doubleArrayOf`,
  etc.

## Loops

- Em programação, **loops** são usados para repetir um bloco de código enquanto uma condição for verdadeira ou enquanto
  houverem elementos a serem percorridos.
- Em **Kotlin**, os principais tipos de loops são: `for`, `while` e `do...while`.

### `for` loop

- Usado geralmente para iterar sobre ranges, arrays, listas ou qualquer estrutura iterável.
- Exemplo com range:
    ```kotlin
    for (i in 0..9) {
      println(i)
    }
    ```
    - `0..9` representa um range de 0 a 9 (inclusive).
- Exemplo com listas:
    ```kotlin
    val name = listOf("Ana", "Bruno", "Carlos")

    for (name in names) {
      println(name)
    }
    ```
- Também podemos acessar o índice com `withIndex()`:
    ```kotlin
    for ((index, name) in names.withIndex()) {
      println("[$index] $name")
    }
    ```

### `while` loop

- Executa um bloco de código **enquanto** a condição for verdadeira.
    ```kotlin
    var i = 0
    while (i < 10) {
      println(i)
      i++
    }
    ```

### `do...while` loop

- Executa o bloco de código **ao menos uma vez**, depois verifica a condição.
    ```kotlin
    var j = 0
    do {
      println(j)
      j++
    } while (j < 10)
    ```

### Controle de fluxo: `break` e `continue`

- `break`: finaliza o loop imediatamente.
- `continue`: pula para a próxima iteração do loop.

- Exemplo com `break`:
    ```kotlin
    for (i in 0..9) {
      if (i == 5) break
      println(i)
    }
    ```

- Exemplo com `continue`:
    ```kotlin
    for (i in 0..9) {
      if (i == 5) continue
      println("Valor: $i")
    }
    ```

### Observações

- Ranges em Kotlin são bem poderosos:
    - `0 until 10` → de 0 até 9 (exclusivo).
    - `10 downTo 1` → de 10 até 1 (decrescente).
    - `0..10 step 2` → de 0 a 10, pulando de 2 em 2.

    ```kotlin
    for (i in 10 downTo 1 step 2) {
      println(i)
    }
    ```

## Funções

- Funções são blocos de código reutilizáveis que executam uma tarefa específica.
- Em Kotlin, funções podem ser declaradas fora de classes (top-level), dentro de classes (como métodos), ou como
  expressões anônimas (lambdas).
- A palavra-chave usada para declarar uma função é `fun`.

### Sintaxe básica

```kotlin
fun functionName(param: Type): ReturnType {
    return valor
}
```

### Funções com retorno `Unit`(sem retorno)

```kotlin
fun printMessage(msg: String): Unit {
    println(msg)
}
```

- O tipo Unit equivale ao void do Java. Pode ser omitido:

```kotlin
fun printMessage(msg: String) {
    println(msg)
}
```

### Funções com valores padrão e argumentos nomeados

- Podemos definir valores padrão para os parâmetros:

```kotlin
fun greet(nome: String = "World") {
    println("Hello, $nome!")
}

greet() // Hello, World!
greet("Fulano") // Hello, Fulano!
```

- Também é possível passar os argumentos fora de ordem, nomeando-os:

```kotlin
fun printData(name: String, age: Int) {
    println("$name is $age years old")
}

printData(age = 30, name = "John")
```

### Funções como expressões

- Podemos simplificar funções com uma única linha usando `=`

```kotlin
fun multiply(a: Int, b: Int) = a * b
```

### Funções anônimas e lambdas

- Funções podem ser passadas como argumentos ou armazenadas em variáveis:

```kotlin
val greeting = { name: String -> "Hello, $name!" }

println(greeting("Maria")) // Hello, Maria!
```

### Funções inline

- Melhora performance evitando a criação de objetos para lambdas.

```kotlin
inline fun doSomething(block: () -> Unit) {
    println("Before")
    block()
    println("After")
}

doSomething {
    println("Inside block")
}
```

### Trailing Lambda Syntax em Kotlin

- Quando uma função tem como último parâmetro uma função (lambda), o Kotlin permite que você passe essa lambda **fora
  dos parênteses**, o que deixa o código mais limpo e legível.

```kotlin
fun operate(a: Int, b: Int, operation: (Int, Int) -> Int): Int {
    return operation(a, b)
}

//normal
val result1 = operate(5, 3, { x, y -> x * y })
println(result1) // 15

//trailing lambda
val result2 = operate(5, 3) { x, y -> x * y }
println(result2) // 15
```

- Você deve passar a lambda dentro dos parêntes apenas quando a lambda estiver como último parâmetro, porque a sintaxe
  do trailing lambda funciona só se a lambda for o último parâmetro.
- Trailing lambda funciona só para a última lambda. A primeira deve estar dentro dos parênteses.

### Funções de Extensão (Extension Functions)

- Funções de extensão permitem **adicionar novas funcionalidades a uma classe existente** sem precisar **herdar** da
  classe ou **modificá-la** diretamente. Elas são muito usadas para tornar o código mais legível, expressivo e
  idiomático em Kotlin.
- Dentro do corpo da função, você pode acessar os membros da instância como se estivesse dentro da própria classe.
- Não altera a classe original. A função é apenas uma “ilusão” de que faz parte da classe.
- Não pode acessar membros **private**  ou **protected** da classe.

```kotlin
// Extension function that checks if an integer is even
fun Int.isEven(): Boolean {
    return this % 2 == 0
}

println(4.isEven()) // Output: true
println(7.isEven()) // Output: false
```

- Ambiguidade com múltiplos `this`.
    - O problema aparece quando usamos outros blocos aninhados que também definem um `this`.
        - Lambdas com receptores (ex: with, apply, run, buildString, etc.).
        - Classes internas ou funções aninhadas.

### Observações

- Kotlin permite sobrecarga de funções (mesmo nome, parâmetros diferentes).
- Também é possível usar vararg para aceitar número variável de argumentos:

```kotlin
fun print(vararg items: String) {
    for (item in items) {
        println(item)
    }
}

print("A", "B", "C")
```

## Enums

- Enums são usados para representar um conjunto fixo de constantes.
- Em Kotlin, enums são mais poderosos que em muitas outras linguagens, pois além de conter valores constantes, podem ter
  propriedades, métodos e até implementar interfaces.

### Sintaxe básica

```kotlin
enum class Day {
    SUNDAY, MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY
}

val today = Day.MONDAY

if (today == Day.MONDAY) {
    println("It's Monday!")
}
```

- Usando com `when`:

```kotlin
when (today) {
    Day.SATURDAY, Day.SUNDAY -> println("Weekend")
    else -> println("Weekday")
}
```

- Enum com propriedades:

```kotlin
enum class Day(val isWeekend: Boolean) {
    SUNDAY(true),
    MONDAY(false),
    TUESDAY(false),
    WEDNESDAY(false),
    THURSDAY(false),
    FRIDAY(false),
    SATURDAY(true)
}

val today = Day.SATURDAY
println("Is weekend? ${today.isWeekend}")
```

- Enum com métodos:

```kotlin
enum class Operation {
    PLUS {
        override fun apply(a: Int, b: Int) = a + b
    },
    MINUS {
        override fun apply(a: Int, b: Int) = a - b
    };

    abstract fun apply(a: Int, b: Int): Int
}

val result = Operation.PLUS.apply(5, 3)
println(result) // Output: 8
```

- Enums implementando interfaces:

```kotlin
interface Printable {
    fun print()
}

enum class Color : Printable {
    RED {
        override fun print() = println("Color is Red")
    },
    GREEN {
        override fun print() = println("Color is Green")
    }
}

Color.RED.print()
Color.GREEN.print()
```

## Null Safety

- Kotlin foi projetado para eliminar os erros de `NullPointerException` (NPE) em tempo de compilação, sempre que
  possível.
- Por padrão, variáveis em Kotlin **não podem ser nulas**, a menos que você explicite isso.

### Declaração de variáveis não nulas (padrão)

```kotlin
var name: String = "John"
name = "Maria" // Ok
name = null    // Compilaton error
```

- Declarando variáveis que aceitam `null`.
    - Usamos ? no tipo para permitir que uma variável seja nula.
    ```kotlin
    var name: String? = "John"
    name = null // Ok
    ```
- Safe Call `(?.)`. Executa uma chamada apenas se a variável não for `null`.

```kotlin
val length = name?.length
println(length) // If name is null, return null
```

- Elvis Operator `(?:)`. Define um valor padrão quando a expressão anterior é `null`.

```kotlin
val length = nome?.length ?: 0
println(length)
```

- Operador Not-Null `(!!)`. Força o Kotlin a assumir que não é `null`.
    - Se for `null`, lança um `NullPointerException`.
    ```kotlin
    val length = nome!!.length
    ```

## Classes

- Classes são a base da programação orientada a objetos em Kotlin.
- Elas podem conter atributos (propriedades) e métodos (funções).
- Kotlin torna a criação de classes mais concisa do que em Java, eliminando muito código boilerplate.

### Sintaxe básica

```kotlin
class Person {
    var name: String = "Your name"
    var age: Int = 0

    fun speak() {
        println("Hello, my name is $name and I'm $age years old")
    }
}

val person = Person()
person.name = "John"
person.age = 30
person.speak()
```

- Construtor primário pode ser definido diretamente na declaração da classe.

```kotlin
class Person(val name: String, var age: Int) {
    fun speak() {
        println("Hello, my name is $name and I'm $age years old")
    }
}

val person = Person("John", 30)
person.speak()
```

- Construtor secundário, usado para fornecer alternativas de construção.

```kotlin
class Pessoa {
    var name: String
    var age: Int = 0

    constructor(name: String, age: Int) {
        this.name = name
        this.age = age
    }

    fun speak() {
        println("Hello, my name is $name and I'm $age years old")
    }
}
```

- Classes com bloco de inicialização `init`:

```kotlin
class Person(val name: String, var age: Int) {
    init {
        println("Create person: $name, $age years old")
    }
}
```

- Propriedades com valor padrão.

```kotlin
class Person(val name: String, var age: Int = 18)
```

### Data Classes

- Em Kotlin, `data class` é uma maneira concisa de criar classes que servem apenas para armazenar dados.
- O compilador gera automaticamente métodos úteis como: `equals()`, `hashCode()`, `toString()`, `copy()`, e os
  `componentN()` para desestruturação.

```kotlin
data class Usuario(val nome: String, val idade: Int)
```

## Interfaces

- Interfaces em Kotlin são contratos que definem **métodos e propriedades** que uma classe pode implementar. Elas são
  muito parecidas com interfaces em Java, mas com algumas melhorias:
    - Podem conter **implementações padrão**.
    - Podem ter **propriedades abstratas** (sem implementação) ou concretas (com `getter`/`setter`).
    - Uma classe pode implementar **múltiplas interfaces** (Kotlin permite herança múltipla via interfaces).

```kotlin
interface Animal {
    fun makeSound() // abstract method
}

class Dog : Animal {

    override fun makeSound() {
        println("Bark!")
    }
}
```

- Interfaces com propriedades:

```kotlin
interface Shape {
    val name: String
    fun area(): Double
}

class Circle(private val radius: Double) : Shape {
    override val name: String = "Circle"

    override fun area(): Double {
        return Math.PI * radius * radius
    }
}
```

## Tratamento de Erros

- Kotlin utiliza tratamento de erros baseado em exceções, assim como Java.
- A diferença é que **todas as exceções em Kotlin são não-verificadas** (*unchecked*), ou seja, o compilador **não exige
  ** tratamento com `try-catch` para exceções específicas.
- O uso de `try`, `catch`, `finally` permite capturar e lidar com exceções em tempo de execução.
- Também é possível usar abordagens mais funcionais com `runCatching`, `getOrElse`, entre outras.

### Exemplo básico com `try-catch`

```kotlin
try {
    val number = "abc".toInt()
    println(number)
} catch (e: NumberFormatException) {
    println("Error: ${e.message}")
}
```

- Usando try como expressão (retorna valor):

```kotlin
val number = try {
    "123".toInt()
} catch (e: NumberFormatException) {
    0
}
println(number) // 123
```

- Abordagem funcional com `runCatching`.
- `runCatching` executa um bloco de código e retorna um objeto do tipo `Result`:

```kotlin
val result = runCatching {
    "abc".toInt()
}

result
    .onSuccess { println("Success: $it") }
    .onFailure { println("Error: ${it.message}") }
```

- Retornando valor padrão com `getOrElse`

```kotlin
val number = runCatching {
    "abc".toInt()
}.getOrElse {
    0
}
println(number) // 0
```

## Programação Orientada a Objetos

- A Programação Orientada a Objetos (OOP) é um paradigma onde o código é organizado em **classes** e **objetos**,
  modelando entidades do mundo real.
- Kotlin é totalmente orientado a objetos e fornece suporte completo a:
    - Classes
    - Objetos
    - Herança
    - Encapsulamento
    - Polimorfismo
    - Abstração
- Esses pilares tornam o código mais modular, manutenível e reutilizável.
  Kotlin traz uma abordagem moderna e concisa para a OOP, sem perder poder expressivo.

### Classes e Objetos

- Uma **classe** é uma estrutura que define **propriedades** (variáveis) e **comportamentos** (funções).  
  Ela funciona como um **molde** para criar objetos.

```kotlin
// This class defines a Person with a name and age
class Person(val name: String, var age: Int) {
    fun introduce() {
        println("Hi, my name is $name and I am $age years old.")
    }
}
```

- Um objeto é uma instância concreta de uma classe.
  Quando você instancia uma classe, cria um objeto com seus próprios dados.

```kotlin
fun main() {
    val person1 = Person("Alice", 25) // Object created from Person class
    person1.introduce()
}
```

### Herança

- Herança permite que uma classe herde os membros (funções e propriedades) de outra.
- Isso promove reutilização de código e especialização.

```kotlin
// Base class
open class Animal {
    open fun makeSound() {
        println("Generic animal sound")
    }
}

// Subclass that inherits from Animal
class Dog : Animal() {
    override fun makeSound() {
        println("Bark")
    }
}

fun main() {
    val animal: Animal = Dog()
    animal.makeSound() // Output: Bark
}
```

### Encapsulamento

- Encapsulamento oculta os detalhes internos de uma classe, permitindo acesso somente através de métodos públicos.
- Isso protege os dados e mantém o controle sobre seu uso.

```kotlin
class BankAccount {
    private var balance: Double = 0.0 // Cannot be accessed directly

    fun deposit(amount: Double) {
        if (amount > 0) {
            balance += amount
        }
    }

    fun getBalance(): Double {
        return balance
    }
}

fun main() {
    val account = BankAccount()
    account.deposit(100.0)
    println("Current balance: ${account.getBalance()}") // Output: 100.0
}
```

- O modificador `private` evita acesso externo direto à variável `balance`.

### Polimorfismo

- Polimorfismo permite que objetos de diferentes tipos respondam de forma diferente a uma mesma chamada de método.
- Em Kotlin, isso ocorre principalmente por meio de herança e interfaces.

```kotlin
open class Shape {
    open fun draw() {
        println("Drawing a shape")
    }
}

class Circle : Shape() {
    override fun draw() {
        println("Drawing a circle")
    }
}

class Square : Shape() {
    override fun draw() {
        println("Drawing a square")
    }
}

fun render(shape: Shape) {
    shape.draw()
}

fun main() {
    render(Circle()) // Output: Drawing a circle
    render(Square()) // Output: Drawing a square
}
```

- O mesmo método `draw()` se comporta de forma diferente dependendo do tipo do objeto.

### Abstração

- Abstração foca apenas nos detalhes essenciais, ocultando a complexidade desnecessária.
- A abstração permite que classes concretas implementem apenas o que for necessário, escondendo detalhes da
  implementação.
- Pode ser feita com interfaces ou classes abstratas.
- Usando classe abstrata:

```kotlin
abstract class Vehicle {
    abstract fun move()
}

class Car : Vehicle() {
    override fun move() {
        println("The car drives on the road")
    }
}

fun main() {

    val vehicle: Vehicle = Car()
    vehicle.move() // The car drives on the road
}
```

- Usando interface:

```kotlin
interface Remote {
    fun turnOn()
    fun turnOff()
}

class TVRemote : Remote {
    override fun turnOn() {
        println("TV is ON")
    }

    override fun turnOff() {
        println("TV is OFF")
    }
}

fun main() {
    val remote: Remote = TVRemote()
    remote.turnOn() // TV is ON
    remote.turnOff() // TV is OFF
}
```

### Herança x Composição

- Quando modelamos o comportamento de objetos em Kotlin (ou qualquer linguagem orientada a objetos), uma das decisões
  mais importantes é: **usar herança ou composição?**
- **Herança** é uma relação do tipo "**é um**" (is-a).
    - Uma **subclasse** herda os comportamentos e atributos de uma **superclasse**, podendo sobrescrevê-los.
    - Use herança quando as classes têm relação clara e forte do tipo "é um".
    - Evite herança se a subclasse começar a ignorar ou sobrescrever tudo da classe pai.

```kotlin
// Superclass
open class Animal {
    open fun makeSound() {
        println("Some generic animal sound")
    }
}

// Subclass inherits Animal
class Dog : Animal() {
    override fun makeSound() {
        println("Bark")
    }
}

fun main() {
    val dog = Dog()
    dog.makeSound() // Output: Bark
}
```

- **Composição** é uma relação do tipo "tem um" (has-a).
    - Você usa outras classes como atributos para construir comportamentos mais flexíveis e modulares.
    - A composição promove baixo acoplamento, reuso e facilita testes e mudanças.
    - Você pode trocar a implementação da composição com facilidade, sem afetar a classe principal.

```kotlin
// Reusable class
class Engine {
    fun start() {
        println("Engine started")
    }
}

// Composed class
class Car(private val engine: Engine) {
    fun drive() {
        engine.start()
        println("Car is driving")
    }
}

fun main() {
    val engine = Engine()
    val car = Car(engine)
    car.drive()
}

```

- Use **herança** apenas quando for inegável que a subclasse é um tipo especializado da superclasse.
- Use **composição** para construir sistemas modulares, flexíveis e desacoplados.

## Solid

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

```kotlin
// This class only handles user persistence
class UserRepository {
    fun save(user: String) {
        println("Saving user: $user")
    }
}

// This class only handles notifications
class NotificationService {
    fun sendEmail(email: String) {
        println("Sending email to $email")
    }
}
```

### O — Open/Closed Principle (Aberto para extensão, fechado para modificação)

- Você deve poder adicionar comportamentos sem modificar o código existente.

```kotlin
// Base interface
interface Operation {
    fun calculate(a: Int, b: Int): Int
}

// New operations can be added without changing existing code
class Addition : Operation {
    override fun calculate(a: Int, b: Int): Int = a + b
}

class Multiplication : Operation {
    override fun calculate(a: Int, b: Int): Int = a * b
}

fun execute(op: Operation, a: Int, b: Int): Int = op.calculate(a, b)
```

- Extensão via *interface/abstração*, sem modificar o código da função `execute`.

### L — Liskov Substitution Principle (Substituição de Liskov)

- Você deve conseguir substituir uma classe pai por qualquer subclasse sem quebrar o comportamento esperado.

```kotlin
open class Bird {
    open fun fly() {
        println("Flying...")
    }
}

class Sparrow : Bird() {
    override fun fly() {
        println("Sparrow is flying")
    }
}

// Violation example
class Ostrich : Bird() {
    override fun fly() {
        throw UnsupportedOperationException("Ostriches can't fly")
    }
}
```

- O código quebra ao substituir `Bird` por `Ostrich`.
- A solução é usar abstrações corretas ou interfaces separadas, ex: `FlyingBird`.

### I — Interface Segregation Principle (Segregação de Interfaces)

- Não force uma classe a implementar métodos que ela não usa.
- Interfaces pequenas e específicas respeitam a coesão e facilitam a manutenção.

```kotlin
// Bad design: too many responsibilities in one interface
interface Worker {
    fun work()
    fun eat()
}

// Good: split responsibilities
interface Workable {
    fun work()
}

interface Eatable {
    fun eat()
}

// Now classes implement only what they need
class Robot : Workable {
    override fun work() {
        println("Robot working")
    }
}

class Human : Workable, Eatable {
    override fun work() {
        println("Human working")
    }

    override fun eat() {
        println("Human eating")
    }
}

```

### D — Dependency Inversion Principle (Inversão de Dependência)

- Dependa de **abstrações**, não de implementações concretas.

```kotlin
// Abstraction
interface MessageService {
    fun send(message: String)
}

// Low-level module
class EmailService : MessageService {
    override fun send(message: String) {
        println("Sending email: $message")
    }
}

// High-level module
class NotificationManager(private val service: MessageService) {
    fun notifyUser(message: String) {
        service.send(message)
    }
}

fun main() {
    val service = EmailService()
    val notifier = NotificationManager(service)
    notifier.notifyUser("Welcome!")
}
```

- A classe `NotificationManager` depende da abstração `MessageService`, não de uma implementação fixa.

## Corroutines

- Coroutines são construções de linguagem (nativas em Kotlin) que permitem executar tarefas de forma assíncrona e não
  bloqueante, sem precisar criar ou gerenciar threads manualmente.
- Imagine que você quer fazer algo demorado (como acessar a internet ou ler um arquivo), mas não quer travar a aplicação
  enquanto espera. Com `Thread.sleep()`, a thread inteira é bloqueada.
- As coroutines resolvem isso: permitem pausar a execução e retomar depois, sem bloquear a thread principal. Isso é
  feito com **funções suspensas (suspend)** e um mecanismo interno chamado **continuation**.
- Quando uma `suspend fun` é chamada, a execução é pausada e o compilador gera um estado interno (como uma máquina de
  estados) chamado *continuation*. Esse estado guarda:
    - Onde a função parou.
    - O que precisa ser retomado depois.
    - Quais dados estavam em uso.
- Esse mecanismo torna possível suspender sem perder o contexto da função.

### Conceitos Fundamentais

| Conceito          | Explicação                                                                 |
|-------------------|----------------------------------------------------------------------------|
| `suspend`         | Marca uma função que **pode suspender sua execução** sem bloquear a thread |
| `launch`          | Inicia uma coroutine que **não retorna resultado**                         |
| `async` / `await` | Usado para iniciar coroutines que **retornam resultado**                   |
| `delay`           | Suspende a execução por um tempo sem bloquear                              |
| `runBlocking`     | Cria um **escopo bloqueante**, usado para testes ou `main()`               |

### suspend

- Marca uma função que pode ser suspensa. Ela não bloqueia a thread: em vez disso, pausa a execução até que uma operação
  esteja pronta.
- Funções `suspend` só podem ser chamadas dentro de outra `suspend` ou `runBlocking`.

```kotlin
suspend fun fetchData(): String {
    delay(1000) // coroutine is suspended here
    return "Data"
}
```

### launch

- Cria uma coroutine que não retorna valor (tipo `Job`). Serve para executar tarefas assíncronas de forma independente.
- Ideal para chamadas sem retorno, como log, salvar dados, etc.

```kotlin
launch {
    delay(500)
    println("Doing background task")
}
```

### async

- Cria uma `coroutine` que retorna um valor `Deferred<T>`. Você pode usar `await()` para recuperar o resultado.
- Use quando quiser rodar múltiplas tarefas em paralelo e aguardar seus resultados.

```kotlin
val value = async {
    doSomething()
}
val result = value.await()
```

### delay

- É como o `Thread.sleep()`, mas não bloqueia a thread. Ela apenas suspende a coroutine e libera a thread para outro
  trabalho.
- Internamente usa um mecanismo chamado `scheduling` baseado em continuations.

### runBlocking

- Cria um escopo bloqueante e é usado somente para testes ou `main()`.
- Ele bloqueia a thread atual até que todas as coroutines dentro dele terminem.
- Não é recomendado para uso em produção (pode travar o sistema).

## Gradle

- Gradle é uma ferramenta de automação de builds moderna, amplamente usada em projetos Kotlin, Java, Android, etc.
- Kotlin DSL (Domain Specific Language) é uma forma de escrever os scripts de configuração do Gradle usando Kotlin ao
  invés da sintaxe Groovy (`build.gradle.kts` em vez de `build.gradle`).
- Um projeto simples com Kotlin DSL tem essa estrutura:

```
my-project/
├── build.gradle.kts     // build script em Kotlin DSL
├── settings.gradle.kts  // define o nome do projeto e subprojetos
├── gradle/
│   └── wrapper/
├── gradlew              // script Linux/macOS
├── gradlew.bat          // script Windows
└── src/
    └── main/
        └── kotlin/
```

- Para compilar um projeto usando gradle: `./gradlew build`.
- Para executar o projeto: `./gradlew run`.
- Para rodar os testes: `./gradlew test`.
