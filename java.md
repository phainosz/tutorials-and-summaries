# Anotaçẽs gerais sobre Java

- [Instalação](#instalação)
- [Geral](#geral)
- [Comandos](#comandos)
- [Condições IFs e Switch](#condições-ifs-e-switch)
- [Arrays](#arrays)

- [Orientação a Objetos](#oop)

## Instalação
- Instalar o **JDK**, java development kit.
- Existem várias maneiras de instalar **Java**, uma delas é no site da [oracle](https://www.oracle.com/java/technologies/downloads/).
- Eu gosto de fazer instalação usando [sdkman](https://sdkman.io/), serve para **Java** e outras ferramentas.

## Geral
- **Java** é uma linguagem de programação robusta e fortemente tipada.
- Usa o paradigma [Orientado a Objeto](#oop).
- **Java** é independente de plataforma, isso significa que podemos criar um código que rode em qualquer plataforma.
- Quando *compilamos* um programa feito em **java**, o *compilador* converte o código java em **bytecode**.
- **JVM**, java virtual machine, é uma especificação que provê um ambiente de execução(runtime environment) para executar **bytecode** e converte para código de máquina.
- **JRE**, java runtime environment, é uma combinação de ferramentas usadas para desenvolver aplicações java. É a implementação da **JVM**. **JRE** não é usado para desenvolvimento e sim para executar código java compilado.
- **JDK**, java development kit, provê as ferramentas para debugar, compilar e executar um programa. Contém todo o ferramental que o **JRE** fornece.
- **Variáveis** são containers para guardar valores para determinados tipos. Ao criar uma *variável*, damos um nome, tipo e valor para ela.
  - Em **java** podemos criar variáveis **primitivas** ou **não-primitivas**
    - *primitivos* incluem: `boolean`, `char`, `byte`, `short`, `int`, `float` e `double`.
    - *não primitivos* incluem *classes*, *interfaces* e *arrays*.
- **Java** possui muitas palavras-chaves(keywords) que foram criadas com um propósito específico e usadas dentro do código.
  - Ex:
    ```java
      public class Hello {
        public static void main(String arg[]) {
          System.out.println("Hello, World");
        }
      }
    ```
    - `class` é uma *keyword* específica para declarar uma classe em **java**.
    - `public` é uma *keyword* que representa um modificador de acesso em **java**.
    - `static` é uma *keyworkd* é usado para indicar que algo pertence à uma classe em si e não a uma instância específica. Facilita o acesso e compartilhamento de recursos.
    - `void` é o tipo de retorno em um *método*, no caso `void` não possui retorno.
    - `main` é um método e nesse caso é o ponto de partidade de execução de uma aplicação **java**.
    - `String[] args ou String args[]` são *argumentos* de entrada passado via linha de comando.
    - `System.out.println()` é uma forma de imprimir dados no console.

## Comandos
- Para compilar, podemos usar o comando `javac`. Ex: `javac Hello.java`.
  - Ao compilar, irá gerar um arquivo `Hello.class`.
- Para executar o arquivo compilado, usar o comando `java Hello`.
  - Irá executar o código contido em `Hello.class`.

## Condições IFs e Switch
- Usados para controle condicional usando uma *variável* ou um valor específico como base.
- Ex `if`:
  ```java
    int age = 20;
    if (age < 18) {
      //...
    } else if (age >= 18 && age < 60) {
      //...
    } else {
      //...
    }
  ```
- Ex `switch`:
  ```java
    String number = 0;
    
    switch (number) {
      case 0:
        System.out.println("0");
        break;
      case 1:
        System.out.println("1");
        break;
      case 2:
        System.out.println("2");
        break;
      default:
        System.out.println("error");
        break;
    }
    
    //or

    String result = switch (day) {
      case 0, 1, 2, 3 -> "low";
      case 4, 5, 6 -> "medium";
      case 7, 8, 9 -> "high";
      default -> "error"
    };
  ```
  
## Arrays
- 



## OOP
- **Programação Orientada a Objetos** organiza o código em uma combinação de diferentes tipos de objetos para incorporar ações que representem o mundo real.
- Usamos atributos e métodos para representar características e 