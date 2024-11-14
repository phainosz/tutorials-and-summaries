# Anotaçẽs gerais sobre Java

- [Instalação](#instalação)
- [Geral](#geral)
- [Comandos](#comandos)
- [Condições IFs e Switch](#condições-ifs-e-switch)
- [Arrays](#arrays)
- [Loops](#loops)
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
- Modificadores de acesso em **java**, servem alterar a acessibilidade ou escopo de: *classe*, *método*, *atributos* e *construtores*.
  - **private** torna visível apenas dentro da classe em que se encontra.
  - **public** torna acessível a todos e em qualquer lugar.
  - **protected** é acesível dentro do mesmo pacote ou fora do pacote através sub-classes.
  - **default** acessível apenas dentro do mesmo pacote, quando não informado o modificador de acesso, *default* é o valor padrão.

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
- **Arrays** são estruturas de dados lineares que guardam elementos do mesmo tipo de dado.
- São alocados de forma contígua em memória, o que significa, é um espaço de memória com o tamanho da estutura, onde cada elemento está alocado sequencialmente em um indice do espaço alocado.
- Cada item é indexado e começa no **index** 0 na maioria das linguagens. Podemos acessar um elemento diretamente através do seu índice.
- Ex:
  ```java
      int[] array = new int[2];
      array[0] = 1;
      array[1] = 2;

      // or array creation with initialization
      int[] array2 = { 1, 2, 3, 4, 5 };
  ```

## Loops
- Em programação, **loops** são essenciais para percorrer uma estrutura de dados, repetir uma sequência de código até uma condição específica.
- Em **Java** temos 3 tipos de **loops**: `for`, `while` e `do while`.
- Ex:
  ```java

    //syntax
    //for(initialization; condition; increment/decrement)
    for (int i = 0; i < 10; i++) {
      //some code...
    }
    
    //while (condition)
    int i = 0;
    while (i < 10) {
      //code to be executed     
      i++;
    }
    
    int j = 0;
    do {
      //code to be executed     
      j++;
    } while (j < 10)
  ```
- Podemos usar algumas keywords que alterar o fluxo de execução do loop, como por exemplo `continue` e `break`.
  ```java
    for (int i = 0; i < 10; i++) {
      if (i == 5) {
        break;//when i value is 5, the whole loop will stop e execute the rest of the code. It will break the loop.
      }
    }

    for (int j = 0; j < 10; j++) {
      if (i == 5) {
        continue;//when i equal to 5, it will not print "after if". Continue moves to the next iteration of the loop, ignoring the rest of the code inside the loop after continue statement is met.
      }
      System.out.println("after if");
    }
  ```

## OOP
- **Programação Orientada a Objetos** organiza o código em uma combinação de diferentes tipos de objetos para incorporar ações que representem o mundo real.
- É um paradigma que usa *objetos* para desenhar sistemas de aplicação, simplificando o processo e a manutenção de código.
- Usamos atributos e métodos para representar características e comportamentos de algo real em formato de cõdigo.
- Para entender OO, precisamos entender alguns conceitos cruciais, mas antes de tudo, entender o que é um *objeto*:
  - Um *objeto* é algo que possui um estado e comportamento.
  - É definido a partir da instância de uma *classe*.
  - Possui um endereço de memória.
- *Classes* são onde criamos e estruturamos *métodos* e *atributos*
- Existem quatro pilares que são importantes para o entendimento de OO, **herança**, **polimorfismo**, **abstração** e **encapsulamento**.
- **Herança** permite a criação de novas classes baseadas em classes existentes. Em vez de criar uma classe do zero, você pode definir uma nova classe que herda atributos e métodos de uma classe já existente.
  - A **herança** facilita o reaproveitamento de código, pois as subclasses herdam funcionalidades comuns da superclasse, evitando duplicação.
  - Além de *reuso* a **herança** traz o **polimorfismo** como benefício.
- **Polimorfismo** permite que objetos de diferentes classes sejam tratados como se fossem da mesma classe base, especialmente quando compartilham uma interface ou herdam de uma superclasse comum. Na prática, isso significa que o mesmo método pode ter diferentes comportamentos dependendo do objeto que o está executando.
  - *Overloading* método com mesmo nome, mas com *parâmetros* diferentes.
  - *Overriding* método com mesmo nome, mesmos  *parâmetros*, mas em um *sub-classe*.
- **Abstração** é usados para focar apenas nos aspectos essenciais de um objeto ou sistema, permitindo criar uma representação simplificada de um conceito.
  - Na prática, é implementado usando *classes* e *métodos* que representam partes importantes de um conceito, sem adicionar complexidade. Frequentemente através de *interfaces* e *classes abstratas* que especificam o que deve ser implementado.
- **Encapsulamento** consiste em ocultar os detalhes internos de implementação de uma classe, expondo apenas o que é necessário para que outros componentes interajam com ela. Em outras palavras, o encapsulamento protege os dados e funcionalidades internos de uma *classe*, permitindo acesso somente através de métodos específicos (chamados *getters* e *setters*, ou *métodos públicos*) que a própria classe define.