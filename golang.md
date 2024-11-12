# Anotaçẽs gerais sobre Golang

- [Instalação](#instalação)
- [Comandos Go](#comandos-go)
- [Primeiros passos](#primeiros-passos)
- [Geral](#geral)
- [Formatação](#formatação)
- [Variáveis](#variáveis)
- [Condições IFs e Switch](#condições-ifs-e-switch)
- [Arrays](#arrays)
- [Slices](#slices)
- [Maps](#maps)
- [Loops](#loops)
- [Structs](#structs)
- [Funções](#funções)
- [Métodos](#métodos)
- [Ponteiros](#ponteiros)
- [Interfaces](#interfaces)
- [Goroutines](#goroutines)
- [Channels](#channels)
- [Testes](#testes)
- [Packages](#packages)
- [Modulos](#modulos)
- [Workspaces](#workspaces)
- [Erros](#erros)
- [Generics](#generics)

## Instalação
- [Golang](https://go.dev/doc/install)
    - Instalação linux
        * Seguir os comandos para remover e extrair o zip baixado
            - `sudo rm -rf /usr/local/go && sudo tar -C /usr/local -xzf ZIP_FILE_GO.tar.gz`
        - Testar com `go version` ou `go env`
        - Talvez precise adicionar o caminho do bin para variaveis de ambientes
            - `nano .profile`
            - Adicionar no final `export PATH=$PATH:/usr/local/go/bin`
            - Rodar o comando para atualiar as variáveis `source .profile`
        - VSCode instalar plugin *Go* e configurar VSCode caso necessário, apertar *Ctrl Shift p*, Go: Install/Update Tools, selecionar todos.
- [Go playground](https://go.dev/play/), usar o go via web.

## Comandos Go
- `go version`
- `go env` lista as variaveis do go.
- `go run` para rodar o projeto.
    - `go run` FILE_NAME - para apenas um package.
    - `go run *.go` quando existir mais de um package main.
- `gofmt` formata o código do projeto.
- `go vet` informa erros de código.
- `go doc` serve para verificar doc de pacotes e funções go.
    - `go doc fmt` mostra informações do pacote fmt.
    - `go doc -src fmt Println` mostra informações do arquivo fonte da função Println do pacote fmt.

## Primeiros passos
- Criar o arquivo `main.go`
- Criar o módulo para a aplicação: `go mod init MODULE_NAME`
- Adicionar o pacote: `package main`
- Criar a função principal: `func main()`
- Como rodar: `go run main.go`

## Geral
- Tipos
    - Números Inteiros, ex: `int, int8, int16, int32, int64, uint, rune(alis int32), byte(alias uint8)`
    - Números decimais, ex: `float32, float64`
    - Texto, ex: `string`
    - Booleanos, ex: `bool`
- Operador curto (*gopher*)
    - Usado para atribuir valor e tipo para variáveis, ex:
        ```go
            name := "A randon name"
        ```
    - Só funciona dentro de codeblocks
    - Apenas para variáveis novas
- Tags nos atributos do struct servem para mudar o nome dos atributos.
  <details>
    <summary>Ex:</summary>

    ```go
    type user struct {
      Id       int    `json:"id"`
      Name     string `json:"name"`
      Username string `json:"username"`
      Phone    string `json:"phone"`
    }
    ```
  </details>
- Go tem suporte a declaração simplificada, semelhante ao usado no loop for, onde a variável é criada no bloco e usada apenas no escopo deste bloco.
  <details>
    <summary>Ex:</summary>

    ```go
    switch day := "monday"; day {
      case "monday":
        fmt.Println("today is monday!")
      case "friday":
        fmt.Println("today is friday!")
      default:
        fmt.Println("day not found!")
    }
    ```
  </details>
- Usar `go env -w` adicionar/alterar variáveis do go, ex: `go env -w GO111MODULE=on`. Para remover usar `go env -u GO111MODULE`.
- Ao trabalhar com repositórios que contenham dependências que estão de forma insegura (casos onde o servidor não possuí certificados ou não faz o uso de https), go fornece uma forma de adicionar hosts que queremos utilizar no nosso código.
    - *GOINSECURE* é definido como uma lista de hosts separados por vírgula, adicionar como variável de sistema.
    - Ex: `go env -w GOINSECURE=github.com,golang.org` habilita download de pacotes inseguros dos hosts informados.
- Para adicionar repositórios privados como dependências em projetos go, é possível adicionar como lista os repositórios e as credencias(se necessário).
    - Usar *GOPRIVATE* e adicionar a lista de hosts e credências(se necessário) como variável do sistema.
    - Ex: `go env -w GOPRIVATE=github.com/company/*` habilita download de pacotes privados dos hosts informados.
- Para fazer build, usar `go build`. Ao usar projetos **Go** com módulos, o nome do módulo será o nome do arquivo gerado após o build.
    - Usar `go build -o <NAME>` para mudar o nome do arquivo gerado no build.
- Ao fazer o build de um projeto, podemos usar a arquitura do sistema atual ou especificar o sistema desejado.
- Para verificar as arquiteturas suportadas, usar `go tool dist list`.
- Para trocar a arquitetura e usar uma diferente, usar o seguinte comando:
    - `GOOS=windows GOARCH=amd64 go build -o app.exe`
    
- Estrutura para projetos **Go**:
    - *cmd* será onde fica a aplicação *main* do projeto.
    - *pkg* é usado para adionar código que poderá ser exportado para uso público. Garanta que tudo está funcionando corretamente neste pacote, pois outros projetos podem importar o seu projeto e fazer o uso do conteúdo de *pkg*.
    - *internal* a estrutura é a mesma que *pkg*, porém é utilizado como código privado, que exportar o seu projeto usando **Go**, não terá acesso.
    - *api* é onde adicionamos definições e especificações para **OpenAPI/Swagger**.
    - *web* componentes específicos de aplicações web, arquivos estáticos como **css** ou **html**.
    - *scripts* diretório com scripts e instruções para construção, instalação, etc.
    - *tests* testes para o projeto.
    - Mais informações [clique aqui](https://github.com/golang-standards/project-layout/blob/master/README_ptBR.md).
    ```
    |---cmd
    |   |---main.go
    |---pkg
    |   |---config
    |   |---utils
    |   |---models
    |   |---routes
    |   |---controllers
    |   |---repositories
    |---internal
    |---api
    |---web
    |   |---index.html
    |   |---css.css
    |---scripts
    |   |---init.sql
    |---tests
    |---go.mod
    |---go.sum
    ```

## Formatação
- Existem casos que queremos modificar o valor de uma string usando formatação. Uma das formas seria usando `fmt.Printf("Oi %s", nome)`
- O **%s** é chamado de verbo de anotação e existem outros com propósitos diferentes.
    - `%v` valor no formato padrão para o tipo do dado passado.
        - `bool:                    %t`
        - `int, int8 etc.:          %d`
        - `uint, uint8 etc.:        %d, %#x if printed with %#v`
        - `float32, complex64, etc: %g`
        - `string:                  %s`
        - `chan:                    %p`
        - `pointer:                 %p`
    - `%T` usado para verificar o tipo da variável.
    - `%t` para booleano, *true* ou *false*.
    - `%b` para valor inteiro base 2(0 ou 1).
    - `%d` para valor inteiro base 10(0-9).
        - `%+d` para mostrar o sinal.
    - `%f` para valor decimal.
    - `%c` para caracteres unicodes, **rune**.
    - `%02d` adiciona zero a esquerda, *2* pode ser alterado para a quantidade de zeros a esquerda.
    - `%s` para strings.
    - `%p` endereço de memória do tipo. **Observação: ao usar em *slice* pega o endereço de memória do primeiro elemento do slice.**
        ```go
        sliceExample := []int{1,2,3}
        fmt.Printf("first element address: %p", sliceExample)//memory address of 0th element (1)
        fmt.Printf("slice adress: %p", &sliceExample)//memory address of slice
        ```
    - [clique aqui](https://pkg.go.dev/fmt) para saber mais.

## Variáveis
- `var` e `const`
- Inferência usando **:=** ex: `name := "Foo`
- Operações em tipos numéricos devem ser do mesmo tipo.

## Condições IFs e Switch
- Seguem o formato a seguir:
  <details>
    <summary>Ex:</summary>

    ```go
    if someVariable {

    } else {

    }
    ```
  </details>
- Podendo usar o if compacto, onde declara a variavel e à atesta, sendo acessível apenas dentro do escopo:
  <details>
    <summary>Ex:</summary>

    ```go
    if number := 10; number > 5 {
        fmt.Println("Maior que 5")
    }
    ```
  </details>
- Para o switch, mesma coisa:
  <details>
    <summary>Ex:</summary>

    ```go
    switch someVariable {
      case 1:
        //do something
      case 2, 3, 4:
        //do something
      default:
        //do default
    }
    ```
  </details>
- No switch, pode-se utilizar o fallthrough para pular para o próximo case. Será executado o case que satisfez a condição e o próximo na sequência:
  <details>
    <summary>Ex:</summary>

    ```go
    switch someVariable {
      case 1:
        //do something
        fallthrough
      case 2, 3, 4:
        //do something
      default:
        //do default
    }
    ```
  </details>
- Pode-se utilizar expressões em troca da condicional do switch:
  <details>
    <summary>Ex:</summary>

    ```go
    value := 5
    switch {
      //switch without condition evaluate true cases
      case (value == 5), (value > 3):
        //do something
      case value < 3:
        //do something
      default:
        //do default
    }
    ```
  </details>

## Arrays
- Sintaxe, `var array [n]T`, *n* é o tamanho e *T* é o tipo.
    - `var array = [50]string{}`, `var array [50]string` ou `var array [5]int = [5]int{1,2,3,4,5}`.
- Para adicionar ou alterar, é da mesma forma convencional: `array[0] = "String"`.
- Tamanho total do array ex: `len(array)`.

## Slices
- É uma abstração do array com tamanho dinâmico.
- Slices são referências de valores, diferente de arrays que são tipos de valores. Isso implica que quando criamos um array e passamos como parametro de uma função, todos os elementos serão copiados, enquanto quando usamos slice, a função recebe a referência em memória do slice.
- Criado igual o array mas sem o tamanho do array, ex: `var slice[]string` ou `var slice = []string{}`.
- Para adicionar no próximo elemento do slice, é utilizado append, ex: `slice = append(slice, "Dado")`. Podendo ser passado n elementos como parametros, ex: `slice = append(slice, "Dado", "Dado2")`.
- Para fazer o slice de um slice, usar os indices desejados: 
  <details>
    <summary>Ex:</summary>

    ```go
    slice := []int{1,2,3,4,5}
    slice2 := slice[0:3]
    //slice2: [1 2 3]
    ```
  </details>
- O slice pode ser simplificado na passagem do indices:
  <details>
    <summary>Ex:</summary>

    ```go
    slice := []int{1,2,3,4,5}
    slice2 := slice[:3]
    //slice2: [1 2 3]
    ```
  ou

    ```go
    slice := []int{1,2,3,4,5}
    slice2 := slice[:]
    //slice2: [1,2,3,4,5]
    ```
  </details>
- Para remover itens de um slice, usar a função `append()` para criar um novo slice a partir dos indices:
  <details>
    <summary>Ex:</summary>
    
    ```go
    slice := []int{1,2,3,4,5}
    slice2 := append(slice[:2], slice[3:]...)//slice[:2] (1,2), slice[3:] (4,5) -> get 1,2 and append with 4,5
    //... the dots is used because append uses only elements of the same type, it's similar to javascript spread operator
    //slice2: [1 2 4 5]
    ```
  </details>
- O slice pode ser criado de outra forma, usando o make([]T, length, cap), ex: `slice := make([]int, 5, 10)`
    - []T é a declaração do tipo do array, ex: `[]int`
    - length é o tamanho inicial do array.
    - cap é a capacidade máxima do array.
- Tomar cuidado com o array subjacente.
## Maps
- É uma collection de chave valor.
- Criado usando chave e valor tipados, ex: `var mymap map[string]string` ou um map vazio `var mymap = make(map[string]string)`.
- Para adicionar no map, ex: `mymap["key"] = value`.
- O range em maps seria o mesmo de arrays e slices, porém o indice se torna a key:
  <details>
    <summary>Ex:</summary>
    
    ```go
    myMap := map[int]string{1: "Um", 2: "Dois"}
    for key, value := range myMap {
      fmt.Println(key, value)
    }
    ```
  </details>
- Para deletar elementos do map, usar delete usando a chave:
  <details>
    <summary>Ex:</summary>
    
    ```go
    myMap := map[int]string{1: "Um", 2: "Dois", 3: "Tres"}
    delete(myMap, 2)
    ```
  </details>

## Loops
- Existe apenas *for* em **GO**, *while* e *doWhile* não existem.
- O mesmo de C ou Java: 
  <details>
    <summary>Ex:</summary>
    
    ```go
    sum := 0
    for i := 1; i < 5; i++ {
      sum += i
    }
    ```
  </details>
- Maneira que se assemelha ao while: 
  <details>
    <summary>Ex:</summary>
    
    ```go
    n := 1
    for n < 5 {
      n *= 2
    }
    ```
  </details>
- Loop infinito:
  <details>
    <summary>Ex:</summary>
    
    ```go
    sum := 0
    for {
      sum++ 
    }
    ```
  </details>
- ForEach range loop:
  <details>
    <summary>Ex:</summary>
    
    ```go
    strings := []string{"hello", "world"}
    for index, element := range strings {
      fmt.Println(index, element)
    }
    ```
  </details>
- Em casos onde o index do ForEach não é necessário, pode utilizar _ para ignorar o indice:
  <details>
    <summary>Ex:</summary>
    
    ```go
    strings := []string{"hello", "world"}
    for _, element := range strings {
      fmt.Println(element)
    }
    ```
  </details>

## Structs
- Funciona de forma semelhante do C.
- Usado como forma de definir multiplos tipos de dados.
- Alternativa para classes em Go.
- Os campos da struct seguem o padrão de nomenclatura para export de dados, pascal case para usar fora do pacote:
  <details>
    <summary>Ex:</summary>
    
    ```go
    type UserData struct {
      firstName       string
      lastName        string
      email           string
      numberOfTickets uint
    }
    ```
  </details>
- Como adicionar valores para struct. Primeiro segue como o nome do campo da struct, segundo como o valor:
  <details>
    <summary>Ex:</summary>
    
    ```go
    var userData = UserData {
      firstName:       firstName,
      lastName:        lastName,
      email:           email,
      numberOfTickets: userTickets,
    }
    ```
  </details>
- Ou de forma simplificada quando o nome do campo é o mesmo do nome da variável:
  <details>
    <summary>Ex:</summary>

    ```go
    var userData = UserData {
      firstName,
      lastName,
      email,
      userTickets,
    }
    ```
  </details>
- Ou adicionar apenas no campo como se fosse um set:
  <details>
    <summary>Ex:</summary>

    ```go
    var userData = UserData{}
    userData.email = "email"
    userData.firstName = "Name"
    ```
  </details>
- Structs anônimos são structs que são criados apenas no escopo do código, mudando de escopos já não são mais utilizáveis:
  <details>
    <summary>Ex:</summary>

    ```go
    func main() {
      anonymouStruct := struct {
        name string
        age  int
      }{
        name: "Test",
        age:  10,
      }
    }
    ```
  </details>
- Go não suporta herança da forma que conhecemos, porém tem uma forma similiar para criar structs.
  <details>
    <summary>Ex:</summary>

    ```go
    type Person struct {
      Name string
      Age  int
    }

    type Worker struct {
      Job string
      Person
    }

    func main() {
      worker := Worker{}

      worker.Name = "Jon"
      worker.Age = 20
      worker.Job = "Developer"
    }
    ```
  </details>
- No exemplo acima, a struct contém um campo sem mencionar o tipo, fazendo com que os campos sejam os mesmos da struct original.
- Em Go podemos fazer o uso de composição:
  <details>
    <summary>Ex:</summary>

    ```go
    type Person struct {
      Name string
      Age  int
    }

    type Worker struct {
      Job string
      Person Person
    }

    func main() {
      person := Person{"Jon", 20}
      worker := Worker{"Developer", person}
    }
    ```
  </details>

## Funções
- A nomenclatura usada no Go é *func*.
- Por padrão parâmetros em Go são *pass by value* o que signifa é que todo parâmetro de função é uma cópia.
- Em casos que não queremos fazer uma cópia do parâmetro, são usados [ponteiros](#ponteiros)
- Funções sem retorno:
  <details>
    <summary>Ex:</summary>

    ```go
    func someFunction() {
        //do something
    }
    ```
  </details>
- Funções com retorno:
  <details>
    <summary>Ex:</summary>

    ```go
    func someFunction() string {
      //do something
      return someString
    }
    ```
  </details>
- Funções com parametros:
  <details>
    <summary>Ex:</summary>

    ```go
    func someFunction(param string) {
      //do something
    }
    ```
  </details>
- Ou com multiplos parametros, que tenham o mesmo tipo, pode ser simplificado.
  <details>
    <summary>Ex:</summary>

    ```go
    func someFunction(param string, param2 string) {
      //do something
    }
    func someFunction2(param, param2 string) {
      //do something
    }
    ```
  </details>
- No Golang, pode ser retornado múltiplos valores:
  <details>
    <summary>Ex:</summary>

    ```go
    func someFunction() (string, int) {
      //do something
      return someString, someInt
    }
    ```
  </details>
- Defer func serve para adiar algo, ele deixa a execução por último.
    - Multiplos defer, funcionam como uma pilha, LIFO.
- Funções anônimas, usadas para serem chamadas apenas uma vez, sem necessidade de criação e nome.
    - Podendo ser criadas com invocação imediata ou invocação apenas quando chamada.
  <details>
    <summary>Ex:</summary>

    ```go
    func main() {
      x := 123

      func(x int) {
        fmt.Println(x*2)
      }(x)

      y := func(x int) {
        fmt.Println(x42)
      }
      
      y(x)
    }
    ```
  </details>
### Métodos
- São funções especificas de um tipo. Podendo ser acessadas apenas por esse tipo:
  <details>
    <summary>Ex:</summary>

    ```go
    type person struct {
      name string
    }

    func (p person) printName() {
      fmt.Print(p.name)
    }

    func main() {
      person := person{"Test"}

      person.printName()
    }
    ```
  </details>
- Podemos usar métodos com a intenção de alterar o valor usando ponteiros:
  <details>
    <summary>Ex:</summary>

    ```go
    type person struct {
      name string
    }

    func (p *person) changeName(name string) {
      p.name = name
    }

    func main() {
      person := person{"Foo"}

      person.changeName("Bar")
    }
    ```
  </details>

## Ponteiros
- São variáveis que apontam para um endereço de memória.
- Um ponteiro declarado mas não dado o valor(`var a *int`), tem valor **nil**.
- Ponteiros são referências de memória. Para lidar com ponteiros, podemos usar dois operadores:
    - **&** que faz a referência do endereço em memória de uma variável. Chamado de *referencing*
    - __\*__  que acessa o valor da variável que o ponteiro aponta. Chamado de *dereferencing*
- Quando queremos passar o endereço de memória de uma variável para um ponteiro, usamos **&**.
  <details>
    <summary>Ex:</summary>

    ```go
    var a int = 1
    var b *int = &a
    ```
  </details>
- No exemplo acima, b aponta para o endereço de memória de a, se usarmos `fmt.Println(*b)` teremos o valor **1** como output.
- Quando usado uma variável para apontar para o endereço de memória, para pegar o valor do endereço de memória, usa *:
  <details>
    <summary>Ex:</summary>

    ```go
    x := 10
    y := &x //& define y with same memory address as x
    fmt.Println(*y) //print y memory address
    ```
  
  Ou

    ```go
    x int := 10
    y *int := &x //& define y with same memory address as x
    fmt.Println(*y) //print y memory address
    ```
  </details>
- Para passar o ponteiro e receber o endereço dentro de uma função:
  <details>
    <summary>Ex:</summary>

    ```go
    x := 0
    changeNumber(&x)

    func changeNumber(number *int) {
      fmt.Println(number) //print memory address
      fmt.Println(*number) //print value
      *number++ //increase value not only local but all variables that points to same memory adress
    }
    ```
  </details>

## Interfaces
- Funciona como um contrato, semelhante em orientação a object, mas sem a necessidade de implementar diretamente:
  <details>
    <summary>Ex:</summary>

    ```go
    package main

    import (
      "fmt"
      "math"
    )

    func main() {
      square := Square{width: 2.0, height: 3.0}
      circle := Circle{radius: 2}
      calculateArea(square)
      calculateArea(circle)
    }

    func calculateArea(shape Shape) {
      fmt.Println(shape.area())
    }

    type Shape interface {
      area() float64
    }

    type Square struct {
      width  float64
      height float64
    }

    func (square Square) area() float64 {
      return square.width * square.height
    }

    type Circle struct {
      radius float64
    }

    func (circle Circle) area() float64 {
      return math.Pi * math.Pow(circle.radius, 2)
    }
    ```
  </details>

## Goroutines
- Gouroutines é a forma que Go trabalha com concorrencia usando algo similar a threads, mas mais leves.
- Ao lidar com concorrência, alguns conceitos precisam ser abordados:
    - *Data race* acontece quando tentamos acessar a mesma variável. Por exemplo, duas threads acessam a mesma variável, uma tenta ler e outra escrever.
    - *Race conditions* acontece quando o tempo ou ordem afeta um pedaço do código.
    - *Deadlock* acontece quando *goroutines* estão esperando e não conseguem prosseguir na execução do código.
- Qualquer função pode se tonar uma goroutine simplesmente usando a palavra chave **go** em frente a função:
  <details>
    <summary>Ex:</summary>

    ```go
    func main() {
      go doSomething()
      doSomething2()
    }

    func doSomething() {
      // do something
    }
    ```
  </details>


## Channels
- *Channels* são uma forma de fazer sincronização em código concorrente.
- Eles nos permitem trasmitir valores entre goroutines.
- A comunicação é semelhante em um cano, tem uma entrada e uma saída. Elas entram e saem na mesma ordem até o channel ser fechado.
- Para adicionar e retirar informação de um channel, precisa ser feito de forma concorrente.
    - Não podendo adicionar e retirar em uma mesma goroutine.
- Para criar um channel, tem duas formas:
  <details>
    <summary>Ex:</summary>

    ```go
    func main() {
      var ch chan string //accepts any type
      
      ch2 := make(chan int)
    }
    ```
  </details>
- *Channels* enviam e recebem dados, usando **<-**:
  <details>
    <summary>Ex:</summary>

    ```go
    func main() {
      ch := make(chan string)

      go speak(ch)

      data := <-ch //read
      //data: 'Hello World!'
    }

    func speak(ch chan string) {
      ch <- "Hello World!" //write
    }
    ```
  </details>
- *Channels* por padrão são bidirecionais, enviam e recebem dados, porém podemos restringir para fazer apenas uma das funções:
  <details>
    <summary>Ex:</summary>

    ```go
    func main() {
      ch := make(chan string)

      go speak(ch)

      data := <-ch //read data from channel
      //data: 'Hello World!'
    }

    func speak(ch chan<- string) {
      //chan<- only sends data
      ch <- "Hello World!"//write danta into channel
    }
    ```
  </details>
- Quando terminamos de usar um canal, este deve ser fechado, usando `close(ch)`.
- Opcionalmente, podemos testar se um canal foi fechado usando um segundo parâmentro como expressão, booleano que indica a situação do canal:
  <details>
    <summary>Ex:</summary>

    ```go
    func main() {
      ch := make(chan string)

      go speak(ch)

      data, ok := <-ch
      //ok is false because channel is oppen

      close(ch)
    }
    ```
  </details>
- Quando um channel não é fechado usando `close(channel)`, pode ocorrer o deadlock, que seria quando um canal parou de enviar informação, mas alguém ainda está ouvindo e esperando por algo a ser enviado.
- Exemplo deadlock:
  <details>
    <summary>Ex:</summary>

    ```go
    func main() {
      channel := make(chan int)

      go loop(channel)

      for {
          number := <-channel
          fmt.Println(number)
      }
      //prints:
      // 0
      // 1
      // 2
      // 3
      // 4
      // fatal error: all goroutines are asleep - deadlock!
      //due to infinte loop, will keep waiting for values, leading to deadlock
    }

    func loop(channel chan int) {
      for i := 0; i < 5; i++ {
          channel<- i
      }
    }
    ```
  </details>
- Para corrigir e não acontecer o deadlock, pode ser verificado se o channel ainda está aberto e fechar quando ele não ser mais necessário.
- Exemplo correção deadlock:
  <details>
    <summary>Ex:</summary>

    ```go
    func main() {
      channel := make(chan int)

      go loop(channel)

      for number := range channel {
        fmt.Println(number)
      }
    }

    func loop(channel chan int) {
      for i := 0; i < 5; i++ {
        channel<- i
      }
      //close channel after sending all values
      close(channel)
    }
    ```
  </details>
- Channels podem ser criados de forma a limitar a quantidade de informação que enviam/recebem dados, chamados de *buffered channels*. Uma vantagem em se fazer isso, seria para não bloquear a thread, um channel só seria bloqueado se o limite de dados enviados chegar no limite do *buffer* ou o channel que lê dados estiver vazio.
    - Para criar um *buffered channel*, usar `channel := make(chan int, 1)` que terá o limite de *buffer* como 1.
- Channels são bidirecionais por padrão, porém podemos usá-los de forma unidirecional:
  <details>
    <summary>Ex:</summary>

    ```go
    package main

    import (
      "fmt"
      "time"
    )

    func main() {
      ch := make(chan int)
      writerChannel(ch)
      readerChannel(ch)

      time.Sleep(time.Second * 1)
    }

    //function that receives a only reader channel and consume all data
    //ch is a only reader channel
    func readerChannel(ch <-chan int) {
      go func() {
        for {
          val, ok := <-ch
          if !ok {
            fmt.Println("Channel closed!")
            break
          }
          fmt.Println(val)
        }
      }()
    }

    //function that receives a only writer channel and write data
    func writerChannel(ch chan<- int) {
      go func() {
        defer close(ch)
        i := 0
        for i < 10 {
          ch <- i
          i++
        }
      }()
    }
    ```
  </details>
- Para fazer a leitura de múltiplos channels, existe um formato que pode ser usado, *select*. Usando *select*, o primeiro channel que enviar valor será feito a leitura.
  <details>
    <summary>Ex:</summary>

    ```go
    package main

    import (
      "fmt"
      "time"
    )

    func main() {
      c1 := make(chan string)
      c2 := make(chan string)

      go func() {
        time.Sleep(1 * time.Second)
        c1 <- "one"
      }()
      go func() {
        time.Sleep(2 * time.Second)
        c2 <- "two"
      }()

      for i := 0; i < 2; i++ {
        select {
        case msg1 := <-c1:
          fmt.Println("received", msg1)
        case msg2 := <-c2:
          fmt.Println("received", msg2)
        }
      }
    }
    ```
  </details>

## Testes
- Para criar testes, o Go disponibiliza ferramentas nativas nos seus pacotes.
- Para rodar os testes, pode ser feito no pacote que contem os testes, `go test`.
- Para rodar todos os testes do projeto, usar `go test ./...`.
- Para rodar com o modo verboso, `go test -v`.
- Para rodar com a cobertura de testes, `go test --cover`.
- Tem um modo que gera um txt com a cobertura de cada pacote. Esse arquivo é gerado e feito a leitura por outro comando Go.
    - Para gerar o arquivo, `go test --coverprofile NOME_ARQUIVO.txt`.
    - Para visualizar a cobertura por cada pacote no terminal, `go tool cover --func=NOME_ARQUIVO.txt`.
    - Para visualizar a cobertura por cada pacote em html, `go tool cover --html=NOME_ARQUIVO.txt`.
- Cada teste deve ter o seguinte formato:
    - Criar o arquivo .go com o respectivo nome `_test.go`.
        - ex: Para o main.go, criar o `main_test.go` no mesmo pacote.
    - Cada teste deve começar com **Test** antes do nome do método e adicionar o parametro para uso das validacoes.
        - ex: `TestMetodoXpto(t *testing.T)`.
    
## Packages
- O pacote main é o principal como o nome já diz. Podendo ser utilizado com varios arquivos .go neste mesmo pacote, a diferença está na forma de rodar, os arquivos precisam ser declarados no `go run main.go xxx.go yyy.go` ou na raiz `go run .`.
- Novos pacotes podem ser criados com outras pastas com o nome do pacote.
  <details>
    <summary>Ex:</summary>

    ```go
    //go mod init example
    //---go.mod---
    module example

    go 1.18

    //---main.go--
    package main

    import "example/printing"

    func main() {
      printing.PrintText("Hello World!")
    }

    //---print.go---
    package printing

    import "fmt"

    func PrintText(text string) {
      fmt.Println(text)
    }
    ```
  </details>
- Para fazer o import de funções ou variáveis de um pacote diferente, basta declarar o nome da função como pascal case.
- Package management:
    - `go get <LIB>` baixa e faz o build do código.
    - `go get -u <LIB>` baixa o código da lib atualizado, caso houver.
    - `go intall <LIB>` faz a compilação da lib.

## Modulos
- Modulos servem para gerenciamento de dependências em projetos Go.
- Modulos são coleções de pacotes indicados dentro do **go.mod**.
- `go mod init <MOD_NAME>` cria um novo modulo.
- `go mod tidy` remove/adiciona dependências em **go.mod**.

## Workspaces
- Nos permitem trabalhar com multiplos modulos simultaneamente.
- Funciona de forma similar a modulos.
- Ajudam para rodar um projeto local com alterações de um módulo dependente. Quando temos um projeto x, que usa o modulo y, porém fizemos alterações no módulo y e ele n está com estas alterações no repositório remoto.
- Para criar um workspace, criar uma pasta que será utilizada como workspace, inicializar o workspace com `go work init`.
- Para adicionar os modulos dentro do workspace, utilizar `go work use ./<MODULE>`.
- Após feito isso, o modulo será inserido no workspace, os modulos que dependem de outro podem ser executado normalmente com as alterações que foram feitas locais.
- Um arquivo contendo os modulos e o workspace será criado após rodar `go work init`, com o nome go.work:
  <details>
    <summary>Ex:</summary>

    ```go
    go 1.18

    use(
      ./module1
      ./module2
    )
    ```
  </details>
- Podem ser criados *workspaces* de forma geral e adicionar uma variável de ambiente, cada *módulo* adicioná-lo ao *workspace*. Para fazer isso,
adicionar *GOWORK* como variável do sistema e indicar o path da pasta. Para verificar o local do *GOWORK*, usar `go env GOWORK` no terminal.

## Erros
- No Go não temos exceções e sim erros, e dessa forma, os erros são tratados de forma diferente.
- Podendo usar o pacotes errors para criar seus erros a partir de `errors.New("Error")`.
- Exemplo usando divisão por 0:
  <details>
    <summary>Ex:</summary>

    ```go
    import (
      "errors"
      "fmt"
    )

    func main() {
      result, err := Divide(4, 0)

      if err != nil {
        fmt.Println(err)
        return
      }

      fmt.Println(result)
    }

    func Divide(a, b int) (int, error) {
      if b == 0 {
        return 0, errors.New("cannot divide by zero")
      }

      return a/b, nil
    }
    ```
  </details>
- Outra forma de customizar o erros, seria utilizando `fmt.Errorf("cannot divide %d by 0", a)`.
- Podemos criar erros e usar em pontos de códigos específicos.
    - Para verificar um erro, o pacote *erros* tem uma função para isso.
  <details>
    <summary>Ex:</summary>

    ```go
    var ErrDivideByZero = errors.New("cannot divide by zero")

    func main() {
      result, err := Divide(4, 0)

      if err != nil {
        switch {
        case errors.Is(err, ErrDivideByZero):
          // Do something with the error
          fmt.Println(err)
        default:
          fmt.Println("no idea!")
        }
        return
      }
      fmt.Println(result)
    }

    func Divide(a, b int) (int, error) {
      if b == 0 {
        return 0, ErrDivideByZero
      }
      return a / b, nil
    }
    ```
  </details>
- Existe dentro de Go, **panic** e **recover** que são interfaces internas similares ao **try catch** conhecido em outras linguagens.

## Generics
- Generics possibilitam o uso de chamadas sem tipagem.
  <details>
    <summary>Ex sem generics:</summary>

    ```go
    package main

    import "fmt"

    func main() {
      fmt.Println(sumInt(1, 1))
      fmt.Println(sumFloat(1.1, 1.1))
    }

    func sumInt(a int32, b int32) int32 {
      return a + b
    }

    func sumFloat(a float32, b float32) float32 {
      return a + b
    }
    ```
  </details>

  <details>
    <summary>Ex generics:</summary>

    ```go
    package main

    import "fmt"

    func main() {
      fmt.Println(sum[int32](1, 1))//inference type when called
      fmt.Println(sum(1.1, 1.1))//let compiler infer the type
    }

    func sum[T int32 | float64](a T, b T) T {
      return a + b
    }
    ```
  </details>

  <details>
    <summary>Ex generics com constraint:</summary>

    ```go
    package main

    import "fmt"

    type number interface {
      int | int32 | float32 | float64 | uint | uint8 //and so on
    }

    func main() {
      fmt.Println(sum(1, 1))
      fmt.Println(sum(1.1, 1.1))
    }

    func sum[T number](a T, b T) T {
      return a + b
    }
    ```
  </details>
    - Podendo também fazer o uso de `"golang.org/x/exp/constraints"`. Contém constraints prontas para uso de generics.
