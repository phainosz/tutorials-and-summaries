# Anotaçẽs gerais sobre Rust

- [Instalação](#instalação)
- [Comandos Rust](#comandos-rust)
- [Conceitos Gerais](#conceitos-gerais)
- [Variáveis](#variáveis)
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
- [Módulos](#modulos)
- [Gerenciamento de Memória](#gerenciamento-de-memória)

## Instalação
- [Site oficial](https://www.rust-lang.org/tools/install)
- [Rust playground](https://play.rust-lang.org/)
- Windows
    - Necessário a instalação do Microsoft C++ Build Tools ou Visual Studio.
- Linux
    - Instalar **rustup** seguindo os passos indicados no site oficial.
        - **rustup** faz a instalação e gerenciamento da linguagem **rust**.
        - Para atulizar a versão do **rust**, usar o comando `rustup update`.
        - Para atulizar a versão do **rustup**, usar o comando `rustup self update`.
- Usando VSCode, instalar as extensões:
    - *rust-analyzer*
    - *crates*
    - *Better TOML*

## Comandos Rust
- `cargo init <NAME_PROJETO>` ou `cargo new <NAME_PROJETO>` para criar um projeto.
- `cargo run` para rodar um projeto.
- `rustc --version` para verificar versão do **Rust** instalada.

## Conceitos Gerais
- Gerenciador de pacotes do **Rust** é o **cargo**.
- **Rust** usa o padrão *snake case*.
- **rustc** é o copilador do **Rust**.
- *match* são expressões similares ao *if* e *switch*, porém eles devem cobrir todas as possiblidades da expressão testada.
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

## Variáveis
- Em **Rust** criação de variáveis e constantes são possíveis usando *let* ou *const*.
- Variáveis em **Rust** são imutáveis por padrão.
- Para variáveis, existe o conceito de mutabilidade, uma variável definida usando *let* pode ser reescrita, porém com algumas ressalvas.
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
- Strings podem ser criadas de dois tipos, usando `String::from("my string")` ou `"my string".to_owned()` e o conceito de *borrowed* usando apenas `let my_string = "my string"` onde terá uma *&str*.
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
- Em *Rust* o conceito de métodos existe e é utilizado usando *impl* e o tipo.
- Ex com *mutable*, *self* e a combinação dos dois:
```rust
impl Book {
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

    Book::show_pages(&book);
    book.show_ratings();
    book.modify_ratings();
    book.show_ratings();
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

pub fn main() {
    let a = Box {
        width: 1,
        height: 2,
        depth: 3,
    };
    println!("Box depth {}", a.width);
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
- Para acessar e manipular, usado da mesma forma que em qualquer *array*, lembrando que sem *mut*, não será possível fazer alterações.
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

## Macros
- *macros* são similares a funções, porém eles expandem para execuções de códigos além da função.
- Para identificar que uma função é um *macro*, ao final da função terá uma *!*, `println!(...)`.

## Atributos

## Modulos
- **Rust** disponibiliza um sistema de *módulos* que separam o código de forma lógica e gerenciam a visibilidade de forma hierarquica.
- *Módulos* podem ser *públicos* ou *privados*, privado como valor padrão, para alterar, usar *pub* em frente para torná-lo público.

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
    - Funciona de forma que o valor da variável é emprestado para ser usado em outro escopo sem que seja limpo ao perder o escopo que ela estava.
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