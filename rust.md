# Anotaçẽs gerais sobre Rust

- [Instalação](#instalação)
- [Comandos Rust](#comandos-rust)
- [Conceitos Gerais](#conceitos-gerais)
- [Variáveis](#variáveis)
- [Strings](#strings)
- [Funções](#funções)
- [Loops](#loops)
- [Métodos](#métodos)
- [Structs](#structs)
- [Tuplas](#tuplas)
- [Arrays](#arrays)
- [Vetores](#vetores)
- [Enum](#enum)
- [Macros](#macros)
- [Atributos](#atributos)
- [Packages e Crates](#packages-e-crates)
- [Módulos](#modulos)
- [Traits](#traits)
- [Lifetime](#lifetime)
- [Gerenciamento de Memória](#gerenciamento-de-memória)

## Instalação

- [Site oficial](https://www.rust-lang.org/tools/install)
- [Rust playground](https://play.rust-lang.org/)
- Windows
    - Para o windows é necessário a instalação de algumas ferramentas de compilação.
        - Instalação usando Microsoft C++ Build Tools com Visual Studio.
        - Instalação usando [msys2](https://www.msys2.org/).
            - Baixar e instalar o **msys2**.
            - Executar os comanados:
                - `pacman -S mingw-w64-x86_64-toolchain` para adicionar o *cc linker*.
                - `pacman -S base-devel` para adicioanr *base-devel*.
            - Após finalizar a etapa do **msys2**, instalar o rust:
                - Executar o instalador e selecionar a opção 2.
                - Selecionar yes.
                - Selecionar opção 2, para instalação customizada.
                    - Informar o campo *Default host tiple?*
                        - `x86_64-pc-windows-gnu`
            - Após instalação do **rust**:
                - Localizar o arquivo *.cargo* em "C:\\Users\\<USER>\\.cargo"
                - Criar um arquivo com o nome de *config*
                - Adicionar como conteúdo e salvar:
                ```
                [target.x86_64-pc-windows-gnu]
                linker = "C:\\msys2\\mingw64\\bin\\gcc.exe"
                ar = "C:\\msys2\\mingw64\\bin\\ar.exe"
                ```
- Linux
    - Instalar **rustup** seguindo os passos indicados no site oficial.
        - **rustup** faz a instalação e gerenciamento da linguagem **rust**.
        - Para atulizar a versão do **rust**, usar o comando `rustup update`.
        - Para atulizar a versão do **rustup**, usar o comando `rustup self update`.
- Para o VSCode, instalar as extensões:
    - *rust-analyzer*
        - Dica: usar configurações do vscode para o projeto.
        - Criar um arquivo *json*, usar `Ctrl + Shift + p` e buscar por *Workspace Setting (json)* do vscode.
        - Adicionar no arquivo *settings.json* a seguinte configuração:
        ```json
        {
            "[rust]": {
                "editor.formatOnSave": true,
                "editor.defaultFormatter": "rust-lang.rust-analyzer"
            }
        }
        ```
    - *crates*
    - *Better TOML*

## Comandos Rust

- `cargo init` cria um novo projeto em uma pasta existente.
- `cargo new <NAME_PROJETO>` cria projeto com o nome informado.
- `cargo run` para rodar um projeto.
- `rustc --version` para verificar versão do **Rust** instalada.
- `rustc <FILE>.rs`para fazer o build de um arquivo **Rust*.
- `cargo check` verifica se o código irá compilar sem gerar um executável.
  _ `cargo build` para fazer o build de um projeto criado com o cargo.
    - Podendo usar a flag *release*, `cargo build --release`, que fará otimizações para o código rodar melhor.
- `cargo test` irá rodar os testes criados.
- `cargo clean` remove os artefatos gerados no *build*.
- `cargo tree` traz a lista completa de depências do projeto.

## Conceitos Gerais

- Gerenciador de pacotes do **Rust** é o **cargo**.
- **Rust** usa o padrão *snake case*.
- **rustc** é o copilador do **Rust**.
- *match* são expressões similares ao *if* e *switch*, porém eles devem cobrir todas as possiblidades da expressão
  testada.
    - Se alguma possibilidade for adicionado, o compilador irá informar o erro ao não cobrir esta nova possibilidade.
    - Quando não quiser testar todas as possibilidades, usar *_* como se fosse o *default* do *switch*.
    - Ex:

```rust
fn main() {
    let some_bool = true;
    match some_bool {
        true => println!("true"),//used , instead of ; because expression is ended with , and a statement is ended with ;
        false => println!("false"),
        //use _ as a default value (not recomended when need all possibilities to be covered)
    }
}
```

- *Cargo.toml* é o arquivo que contém metadados do seu projeto rust, assim como suas dependências.
- Documentação em **Rust** é gerado com *///* e a descrição. Para gerar a documentação, usar o comando `cargo doc`ou
  `cargo doc --open`para visualizar
- Exitem alguns formatos de retorno no **Rust** que ajudam a representar dados.
    - *Option*, usado quando pode existir ou não o dado retornado.
        - Pode ser usado *match* para verificar qual foi o retorno.
          -Ex:
        ```rust
        enum Option<T> {
            None,
            Some(T),
        }
        ```        
    - *Result* usado para retornar dados ou erros esperados que possam ser tratados.
        - Ex:
        ```rust
        enum Result<T, E> {
            Ok(T),
            Err(E),
        }
        ```
- Existe o operador *?* no **Rust**, ele é utilizado para retornar dados dos tipos *Result* e *Option* de forma
  simplificada.
    - Ex:
        ```rust
        #[derive(Debug)]
        enum Direction {
            Up,
            Down,
        }

        fn get_direction(value: &str) -> Result<Direction, String> {
            match value {
                "up" => Ok(Direction::Up),
                "down" => Ok(Direction::Down),
                _ => Err("direction invalid!".to_owned()),
            }
        }

        fn print_direction(dir: &Direction) {
            println!("picked direction {:?}", dir);
        }

        fn pick_direction(input: &str) -> Result<(), String> {
            let dir = get_direction(input)?;//? operator, if Err it will return from this line, if Ok the code will continue
            print_direction(&dir);
            Ok(())//return statement wihtou return and ;
        }

        fn main() {
            let dir = pick_direction("up");
            println!("{:?}", dir);
        }
        ```
- *Crates* em **Rust** são como libs externas que são adicionados e utilizadas nos projetos.
    - Usando *cargo*, elas ficam no arquivo em *Cargo.toml*.
    - [crates.io](https://crates.io/) é o site oficial do **Rust** para crates.
- Usar **Clippy** como ferramenta de *lint* para os projetos **Rust**.
    - Para adicionar *clippy* usar o comando: `rustup component add clippy`.
    - Verificar o projeto com `cargo clippy`, similar ao `cargo check`.

## Variáveis

- Em **Rust** criação de variáveis e constantes são possíveis usando *let* ou *const*.
- Variáveis em **Rust** são imutáveis por padrão.
- Para variáveis, existe o conceito de mutabilidade, uma variável definida usando *let* pode ser reescrita, porém com
  algumas ressalvas.

```rust
fn main() {
    let x = 1;
    x = 3 //here will crash at compile time
    //to rewrite x use this concept called shadowing
    let x = 2;
    //or using mut
    let mut x = 3;
}
```

- Os tipos de variáveis seguem o padrão encontrado em outras linguagens, variando em tamanhos e seus tipos.
- Inteiros: `i8 i16 i32 i64 i128 u8 u16 u32 u64 u128`
- Decimais: `f32 f64`
- Booleanos: `bool`
- Characteres: `char`
- Strings podem ser criadas de dois tipos, usando `String::from("my string")` ou `"my string".to_owned()` e o conceito
  de *borrowed* usando apenas `let my_string = "my string"` onde terá uma *&str*.
- Variáveis podem ser convertidas quando não são compatíveis, usando *as*.
    - Ex:

```rust
fn main() {
    multiply(1.1, 2);
}

fn multiply(x: f32, y: u16) {
    println!("{}", x as f64 * y as f64);
}
```

## Strings

- Em **Rust** exitem alguns tipos de *strings*, sendo a mais comuns **String** e **&str**.
- **String** o valor é *owned*, enquanto o **&str** é *borrowed*.
- Ex:

```rust
fn print(data: &str) {
    println!("{:?}", data);
}

fn main() {
    print("a string of &str");
    let owned_string = "owned string".to_owned();
    let another_owned = String::from("another owned");
    print(&owned_string);
    print(&another_owned);
}
```

## Funções

- A declaração de funções em **Rust** usa-se *fn* como palavra chave.
- Para declarar uma função com retorno, usar `->` e indicar qual o tipo de retorno.
- Ex:

```rust
fn my_function() {
    println!("{}", hello_world());
}

fn hello_world() -> String {
    //example when we don't need return and ;
    String::from("Hello World!")
}

fn main() {
    my_function();
}
```

- Funções anônimas ou *closures* são funções sem nome que podem ser usadas como argumentos de outras funções ou como
  execução de função invocada.
- Ex:

```rust
fn main() {
    let add = |a: i32, b: i32| -> i32 {
        a + b
    };
    //or
    let add = |a, b| a + b;
    let sum = add(1, 1);
    println!("{sum}");
}
```

## Loops

- Usados para fazer iterações.
- *loop*, *while* e *for* são os tipos de loops em **rust**.
- *loop* é infinito, podendo ser parado com *break*. Ex:

```rust
fn main() {
    let mut value = 1;
    loop {
        if value > 3 {
            println!("end");
            break;
        }
        println!("looping");
        value = value + 1;
    }
}
```

- *while* segue o mesmo padrão de outras linguagens. Ex:

```rust
fn main() {
    let mut value = 1;
    while value <= 3 {
        println!("looping");
        value = value + 1;
    }
    println!("end");
}
```

- *for* pode ser usado com *iterators* ou com um *range*. Ex:

```rust
fn main() {
    for i in 1..11 {
        println!("{i}");
        //1 is inclusive and 11 is exclusive
        //use 1..=11 for a range that is inclusive on both ends
    }
}
```

## Métodos

- Em *Rust* o conceito de métodos é um pouco diferente, implementar funcionalidades em tipos utilizado usando *impl*.
- Ex:

```rust
struct Book {
    pages: i32,
    rating: i32,
}

impl Book {
    fn new() -> Self {
        //Self is the same as Book or in other cases the type that is implementing
        Self {
            pages: 100,
            rating: 8,
        }
    }

    fn show_pages(book: &Book) {
        println!("Number of pages {}", book.pages);
    }

    fn show_ratings(&self) {
        println!("Ratings {}", self.rating);
    }

    fn modify_ratings(&mut self) {
        self.rating = 15;
    }
}

fn main() {
    let mut book = Book {
        pages: 900,
        rating: 5,
    };
    
    let book2 = Book::new();

    Book::show_pages(&book);
    book.show_ratings();
    book.modify_ratings();
    
    Book::show_pages(&book2);
    book2.show_ratings();
}
```

## Structs

- São usados para definir multiplos tipos de dados.
- Ex:

```rust
struct Box {
    width: i32,
    height: i32,
    depth: i32,
}

fn main() {
    let a = Box {
        width: 1,
        height: 2,
        depth: 3,
    };
    println!("Box depth {}", a.width);
}
```

- *Structs* podem ser usados com *match* para verificar valores.
- Ex:

```rust
struct Box {
    width: i32,
    height: i32,
    depth: i32,
}

fn main() {
    let box1 = Box {
        width: 1,
        height: 2,
        depth: 3,
    };
    
    match box1 {
        Box {width: 1, height, depth} => println!("width of 1 and height is {0:?} and depth {1:?}", height, depth),//width: 1 verify width with value 1
        Box {width, ..} => println!("width of the box is {:?}", width),//.. the dots is to ignore other atributes
    }
}
```

## Tuplas

- São similares a *struct*, servem para armazenar dados, porém dados do mesmo tipo.
- Muito usados em retornos de *funções*.
- Ex:

```rust
fn main() {
    let numbers = tuple_number();
    println!("First number {}", numbers.0);
    println!("Second number {}", numbers.1);
    println!("Third number {}", numbers.2);

    //or using destructuring
    let (x,y,z) = tuple_number();
    println!("First number {}", x);
    println!("Second number {}", y);
    println!("Third number {}", z);   
}

fn tuple_number() -> (i8, i8, i8) {
    return (1,2,3);
}
```

## Arrays

- *Arrays* são usados para manipular listas de informações de um determinado tipo com tamanho fixo.
- Sintaxe: `let years:[i32; 3] = [2000, 2001, 2002]`, `i32` é o tipo e `3` é o tamanho.
- Para acessar e manipular, usado da mesma forma que em qualquer *array*, lembrando que sem *mut*, não será possível
  fazer alterações.
- Para iterar em um *array*, ex:

```rust
fn main() {
    let years: [i32; 3] = [2000, 2001, 2002];

    for year in years.iter() {
        println!("Year {}", year);
    }
}
```

## Vetores

- *Vetores* são usados para manipular listas de informações de um determinado tipo com tamanho dinâmico.
- Contemplam maior funcionalidades como adicionar mais itens no *vetor*, remover, etc.
- Ex:

```rust
fn main() {
    let mut years = Vec::new();
    //or vec![2000,2001];
    years.push(2000);
    years.push(2001);
    years.push(2002);
    years.push(2003);

    for year in years {
        println!("Year {}", year);
    }

    //using macros to create a vector
    let years = vec![2020,2021,2022];//vec! will expand the code to do similar as Vec::new and push items
    for year in years {
        println!("Year {}", year);
    }
}
```

## Enum

- Dados que podem ser usados como variantes.
- Ex:

```rust
enum Direction {
    Up,
    Down,
    Left,
    Right
}

fn main() {
    let go = Direction::Up;
    match go {
        Direction::Up => println!("Up"),
        Direction::Down => println!("Down"),
        Direction::Left => println!("Left"),
        Direction::Right => println!("Right"),
    }
}
```

- Enum podem ser usados com dados adicionais e receber parâmetros como informações.
- Ex:

```rust
enum Discount {
    Percent(i32),
    Flat(i32),
}

fn main() {
    let flat = Discount::Flat(2);
    
    match flat {
        Discount::Flat(2) => println!("flat discount 2"),
        Discount::Flat(ammount) => println!("flat discount of {:?}", ammount),
        Discount::Percent(another_discount) => println!("another value {:}", another_discount),//could change Discount::Percent(another_discount) by _
    }
}
```

## Macros

- *macros* são similares a funções, porém eles expandem para execuções de códigos além da função.
- Para identificar que uma função é um *macro*, ao final da função terá uma *!*, `println!(...)`.
- Exemplo de *macros*:
    - `dbg!(...)` usado para inspecionar códigos durante desenvolvimento.
    - `format!(...)` faz interpeloação de strings. Usado de forma similar ao `println!(...)` porém retorna o valor como
      string.
    - `incluse_str!(...)` insere dados de um arquivo para o código. O arquivo usa o src como diretório de partida.
    - `env!(...)` configura uma variável de ambiente para o código.
    - `todo!(...)` código que falta ser finalizado.
    - `unreachable!(...)` indica que um ponto do código não deverá ser executado.

## Atributos

- *Atributos* em **Rust** são pequenos pedaços de código que fornecem informações para o compilador.
- Syntax, `#[attribute]` para atributos externos e `#![attribute]`para atributos internos.
- Ex:

```rust
//Inner attributes
//remove warning for dead code and unused variables
#![allow(dead_code)]
#![allow(unused_variables)]

struct Struct1 {}
struct Struct2 {}
struct Struct3 {}

fn main() {
    let char1 = 'ん'; // variables unused
    let char2 = ';';
    let some_str = "I'm just a regular &str";
    let some_vec = vec!["I", "am", "just", "a", "vec"];
}
```

## Packages e Crates

- *Crates* é a menor parte do código em **Rust**, quando compilado um arquivo *.rs*, o compilador considera este arquivo
  como um *crate*.
- *Crates* podem ser criado de duas formas: *binário* ou *biblioteca*:
    - *Binário* são programas que podem ser compilados e rodados, devem possuir uma função *main* que define o que será
      executado.
    - Um pacote pode ter múltiplas *crates* do tipo *binário* dentro de *src/bin*.
- *Biblioteca* não possuem função *main* e não compilam para executáveis. São usados como funcionaldiades para serem
  compartilhadas com outros projetos.
- *Package* é um agrupamento de um ou mais *crates*.
- *Package* contém um arquivo `Cargo.toml` que descreve como fazer o build dos *crates*.

## Modulos

- **Rust** disponibiliza um sistema de *módulos* que separam o código de forma lógica e gerenciam a visibilidade de
  forma hierarquica.
- *Módulos* podem ser *públicos* ou *privados*.
- Por padrão, a acessibilidade em **Rust** é dada como private, para tornar público, precisa especificar com *pub*.
- *Módulos* podem ser internos e externos.
- Exemplo *módulo* interno:

```rust
mod math {
    //the function is private without pub modifier
    pub fn sum(a: i32, b: i32) -> i32 {
        a + b
    }
}

fn main() {
    let sum_result = math::sum(1,2);
    println!("result of the sum {:?}", sum_result);
}
```

- Exemplo *módulo* externo:
- Arquivo `main.rs`

```rust
mod math;

fn main() {
    let sum_result = math::add(1, 2);
    println!("result is {:?}", sum_result);
}
```

- Arquivo `math.rs`

```rust
pub fn add(first:i32, second:i32) -> i32 {
  first + second
}
```

- Se um *módulo* tiver outros *módulos* dentro, o formato fica um pouco diferente:

```
|---main.rs
|---math.rs
|---math
|    |---add.rs
```

- No arquivo `main.rs` teríamos a declaração do *módulo* `mod math;`
- No arquivo `math.rs` teríamos a declaração do *módulo* `mod add;`
- Na pasta `math.rs` teríamos os *módulos* que estão dentro do *módulo* **math**.
- Cada arquivo dentro da pasta **math** seria um *módulo* e precisaria ser declarado em `math.rs`

## Traits

- *Traits* servem para definir funcionalidades para certos tipos em **Rust**.
- Ex:

```rust
trait Printer {
    fn print(&self);
}

struct Console;

impl Printer for Console {
    fn print(&self) {
        println!("printing with console");
    }
}

fn print(printer: impl Printer) {
    printer.print();
}

fn main() {
    print(Console{});
    //or
    let console = Console{};
    console.print();
}
```

- Podemos ter um comportamento padrão em alguns casos com *trait*.
- O padrão pode ou não ser sobreescrito, vai ser utilizado de acordo com o código escrito.
- Ex:

```rust
trait Printer {
    fn print(&self) {
        println!("default printing");
    }
}

struct Console;

impl Printer for Console {}

fn main() {
    let console = Console{};
    console.print();
}
```

- *Traits* podem ser usadas como parâmetro de *funções*.
- Ex:

```rust
struct Person {
    name: String,
}

trait Printer {
    fn print(&self);
}

impl Printer for Person {
    fn print(&self) {
        println!("Hello {}", self.name);
    }
}

//print using Printer trait
//if more traits is necessary to use here, the function can be like this: 
//fn print_anything<T: Printer + AnotherTrait>(printer: &T)
fn print_anything<T: Printer>(printer: &T) {
    printer.print();
}

fn main() {
    let person = Person{name: "Jhon".to_owned(),};
    print_anything(&person);
}
```

## Lifetime

- É algo semelhante a *generics*.
- Servem para garantir o que a referência de um tipo é válida no tempo que é necessário.
- Toda referência em **Rust** tem um *lifetime* válido de forma implicita.
- As anotações para *lifetime* possuem uma sintaxe simples que é possível identificar ao encontrar **'** e geralmente
  uma letra na sequência, `&'a ...`.
- Ex 1:

```rust
fn main() {
    let my_string = get_string();
    println!("{}", my_string);
}

//expected lifetime in return parameter
//consider using fn get_string() -> &'static str
fn get_string() -> &str {//missing lifetime specifier, this function's return type contains a borrowed value, but there is no value for it to be borrowed from
    "string"
}//at the end of this function, the value "string" will be dealocated
```

- Ex 2 com a correção do exemplo 1:

```rust
fn main() {
    let my_string = get_string();
    println!("{}", my_string);
}

fn get_string<'a>() -> &'a str {
    "string"
}
```

- Ex 3 usando *static* *lifetime*:

```rust
fn main() {
    let my_string = get_string();
    println!("{}", my_string);
}

fn get_string() -> &'static str {
    "string"
}
```

- *static lifetime* é um tipo especial de *lifetime* que dura por todo o tempo que a aplicação durar.
- Quando temos mais de um parâmetro, podemos ter mais de um *lifetime* e especificar cada um em seus parametros e no
  retorno.
- Ex:

```rust
fn main() {
    let my_string = get_string("first", "second");
    println!("{}", my_string);
}

fn get_string<'a, 'b>(x: &'a str, y: &'b str) -> &'a str {
    x
}
```

## Gerenciamento de Memória

- **Rust** não possui um *garbage collector*.
- Para gerenciamento de memória, **Rust** usa um sistema chamado de *Ownership*.
- *Ownership*:
    - Funciona de forma que apenas um local possa ser o dono de uma variável.
    - Quando o dono desta variável sai do escopo, o valor será limpo da memória.
    - Toda variável e seu valor devem ter um dono.
    - Ex:

```rust
fn main() {
    let years = vec![2000, 2001, 2002];//this scope owns years
    get_years(years);//ownership transfered to get_years()

    println!("Year {}", years[0]);//compile error: value borrowed here after move
}

fn get_years(years: Vec<i32>) {
    for year in years {
        println!("Year {}", year)
    }
}//years is cleaned from memory
```

- Para estas situações, **Rust** apresenta o conceito chamado de *References & Borrowing*.
- *References & Borrowing*:
    - Funciona de forma que o valor da variável é emprestado para ser usado em outro escopo sem que seja limpo ao perder
      o escopo que ela estava.
    - O dono é o responsável por fazer a limpeza assim que perde o escopo.
    - Para usar este conceito de emprestar a referência do valor, usar *&*.
    - Ex:

```rust
fn main() {
    let years = vec![2000, 2001, 2002];
    get_years(&years);//borrow years to get_years

    println!("Year {}", years[0]);//compiled successful
}

fn get_years(years: &Vec<i32>) {//value of years borrowed here
    for year in years {
        println!("Year {}", year)
    }
}
```