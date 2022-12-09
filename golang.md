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
- [Channels](#canais-channel)
- [Testes](#testes)
- [Packages](#packages)
- [Modulos](#modulos)
- [Workspaces](#workspaces)
- [Erros](#erros)

## Instalação
- [Golang](https://go.dev/doc/install)
    - Instalação linux
        * Seguir os comandos para remover e extrair o zip baixado
            - `sudo rm -rf /usr/local/go && tar -C /usr/local -xzf ZIP_FILE_GO.tar.gz`
        - Testar com `go version` ou `go env`
        - Talvez precise adicionar o caminho do bin para variaveis de ambientes
            - `gegit .profile`
            - Adicionar no final `export PATH=$PATH:/usr/local/go/bin`
            - Rodar o comando para atualiar as variáveis `source .profile`
- [Go playground](https://go.dev/play/), usar o go via web.

### Comandos Go
- go version
- go env
    - lista as variaveis do go
- go run
    - go run FILE_NAME - para apenas um package
    - go run *.go - quando existir mais de um package

### Primeiros passos
- Criar o arquivo main.go
- Criar o módulo para a aplicação: `go mod init MODULE_NAME`
- Adicionar o pacote: `package main`
- Criar a função principal: `func main()`
- Como rodar: `go run main.go`

### Geral
- Tipos
    - Números Inteiros, ex: int, int8, int16, int32, int64, uint, rune, byte
    - Números decimais, ex: float32, float64
    - Texto, ex: string
    - Booleanos, ex: bool
- Operador curto (gopher)
    - Usado para atribuir valor e tipo para variáveis, ex:
        ```go
            name := "A randon name"
        ```
    - Só funciona dentro de codeblocks
    - Apenas para variáveis novas
- Json marshal e unmarshal, necessita do uppercase para funcionar.
- Tags nos atributos do struct servem para mudar o nome dos atributos.
- Go tem suporte a declaração simplificada, semelhante ao usado no loop for, onde a variável é criada no bloco e usada apenas no escopo deste bloco, ex:
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
- Usar `go env -w` adicionar/alterar variáveis do go, ex: `go env -w GO111MODULE=on`. Para remover usar `go env -u GO111MODULE`.
- Ao trabalhar com repositórios que contenham dependências que estão de forma insegura (casos onde o servidor não possuí certificados ou não faz o uso de https), go fornece uma forma de adicionar hosts que queremos utilizar no nosso código.
    - *GOINSECURE* é definido como uma lista de hosts separados por vírgula, adicionar como variável de sistema.
- Para adicionar repositórios privados como dependências em projetos go, é possível adicionar como lista os repositórios e as credencias(se necessário).
    - Usar *GOPRIVATE* e adicionar a lista de hosts e credências(se necessário) como variável do sistema.
- Para fazer build, usar `go build`. Ao usar projetos **Go** com módulos, o nome do módulo será o nome do arquivo gerado após o build.
    - Usar `go build -o <NAME>` para mudar o nome do arquivo gerado no build.
- Estrutura para projetos **Go**:
    - *cmd* será onde fica a aplicação *main* do projeto.
    - *pkg* é usado para adionar código que poderá ser exportado para uso público.
    - *internal* funciona de forma semelhante ao *pkg*, porém é utilizado como código privado.
```
|---cmd
|---pkg
|    |---config
|    |---utils
|    |---models
|    |---routes
|    |---controllers
|---internal
|---go.mod
|---go.sum
```

### Formatação
- Existem casos que queremos modificar o valor de uma string usando formatação. Uma das formas seria usando `fmt.Printf("Oi %s", nome)`
- O **%s** é chamado de verbo de anotação e exitems outros com propósitos diferentes, para saber mais [clique aqui](https://pkg.go.dev/fmt)

### Variáveis
- var, const
- tipos int, int8, uint, string, float ...
- Inferência usando := ex: `name := "Paulo`
- Operações em tipos numéricos devem ser do mesmo tipo

### Condições IFs e Switch
- Seguem o mesmo formato, apenas muda o fato de usar () após o if, ex:
```go
if someVariable {

} else {

}
```
- Podendo usar o if compacto, onde declara a variavel e à atesta, sendo acessível apenas dentro do escopo, ex:
```go
if number := 10; number > 5 {
    fmt.Println("Maior que 5")
}
```
- Para o switch, mesma coisa, ex:
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
- No switch, pode-se utilizar o fallthrough para pular para o próximo case. Será executado o case que satisfez a condição e o próximo na sequência, ex:
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
- Pode-se utilizar expressões em troca da condicional do switch, ex:
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

### Arrays
- Sintaxe: `var array = [50]string{}` ou `var array [50]string`
- Para adicionar, é da mesma forma convencional: `array[0] = "String"`
- Tamanho total do array ex: `len(array)`

### Slices
- É uma abstração do array com tamanho dinâmico
- Criado igual o array mas sem o tamanho do array, ex: `var slice[]string` ou `var slice = []string{}`
- Para adicionar no próximo elemento do slice, é utilizado append, ex: `slice = append(slice, "Dado")`. Podendo ser passado n elementos como parametros, ex: `slice = append(slice, "Dado", "Dado2")`
- Para fazer o slice de um slice, usar os indices desejados, ex: 
```go
    slice := []int{1,2,3,4,5}
    slice2 := slice[0:3]
    //ira retornar: [1 2 3]
```
- O slice pode ser simplificado na passagem do indices, ex:
```go
    slice := []int{1,2,3,4,5}
    slice2 := slice[:3]
    //ira retornar: [1 2 3]
```
- ou
```go
    slice := []int{1,2,3,4,5}
    slice2 := slice[:]
    //ira retornar: [1,2,3,4,5]
```
- Para remover itens de um splice, usar a função append() para criar um novo slice a partir dos indices, ex:
```go
    slice := []int{1,2,3,4,5}
    slice2 := append(slice[:2], slice[3:]...) 
    //... é usado pois o append espera elemento do mesmo tipo do slice, semelhante ao spread do javascript
    //ira retornar: [1 2 4 5]
```
- O slice pode ser criado de outra forma, usando o make([]T, length, cap), ex: `slice := make([]int, 5, 10)`
    - []T é a declaração do tipo do array, ex: `[]int`
    - length é o tamanho inicial do array
    - cap é a capacidade máxima do array
- Tomar cuidado com o array subjacente.
### Maps
- É uma collection de chave valor
- Criado usando chave e valor tipados, ex: `var mymap map[string]string` ou um map vazio `var mymap = make(map[string]string)`
- Para adicionar no map, é utilizado append, ex: `mymap["key"] = value`
- O range em maps seria o mesmo de arrays e slices, porém o indice se torna a key, ex:
```go
myMap := map[int]string{1: "Um", 2: "Dois"}
for key, value := range myMap {
    fmt.Println(key, value)
}
```
- Para deletar elementos do map, usar delete usando a chave, ex:
```go
myMap := map[int]string{1: "Um", 2: "Dois", 3: "Tres"}
delete(myMap, 2)
for key, value := range myMap {
    fmt.Println(key, value)
}
```

### Loops
- Apenas for existe no Go, while, doWhile não existem
- O mesmo de C ou Java, ex: 
```go
sum := 0
for i := 1; i < 5; i++ {
    sum += i
}
```
- Maneira que se assemelha ao while, ex: 
```go
n := 1
for n < 5 {
    n *= 2
}
```
- Loop infinito, ex:
```go
sum := 0
for {
    sum++ 
}
```
- ForEach range loop, ex:
```go
strings := []string{"hello", "world"}
for index, element := range strings {
    fmt.Println(index, element)
}
```
- Em casos onde o index do ForEach não é necessário, pode utilizar _ para ignorar o indice, ex:
```go
strings := []string{"hello", "world"}
for _, element := range strings {
    fmt.Println(element)
}
```

### Structs
- Funciona de forma semelhante do C
- Usado como forma de definir multiplos tipos de dados
- Alternativa para classes em Go
- Os campos da struct seguem o padrão de nomenclatura para export de dados, pascal case para usar fora do pacote.
- Ex: 
```go
type UserData struct {
	firstName       string
	lastName        string
	email           string
	numberOfTickets uint
}
```
- Como adicionar valores para struct. Primeiro segue como o nome do campo da struct, segundo como o valor, ex:
```go
var userData = UserData {
		firstName:       firstName,
		lastName:        lastName,
		email:           email,
		numberOfTickets: userTickets,
	}
```
- Ou de forma simplificada
```go
var userData = UserData {
		firstName,
		lastName,
		email,
		userTickets,
	}
```
- Ou adicionar apenas no campo como se fosse um set
```go
var userData = UserData{}
	userData.email = "email"
	userData.firstName = "Name"
```
- Structs anônimos são structs que são criados apenas em código, sem poderem ser utilizados em outros trechos de código, ex:
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
- Go não suporta herança da forma que conhecemos, porém tem uma forma similiar para criar structs.
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
- No exemplo acima, a struct contém um campo sem mencionar o tipo, fazendo com que os campos sejam os mesmos da struct original.
- Em Go podemos fazer o uso de composição, ex:
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

### Funções
- A nomenclatura usada no Go é func.
- Funções sem retorno, ex:
```go
func someFunction() {
    //do something
}
```
- Funções com retorno, ex:
```go
func someFunction() string {
    //do something
    return someString
}
```
- Funções com parametros, ex:
```go
func someFunction(param string) {
    //do something
}
```
- Ou com multiplos parametros, que tenham o mesmo tipo, pode ser simplificado
```go
func someFunction(param string, param2 string) {
    //do something
}
func someFunction2(param, param2 string) {
    //do something
}
```
- No Golang, pode ser retornado múltiplos valores, ex:
```go
func someFunction() (string, int) {
    //do something
    return someString, someInt
}
```
- Defer func serve para adiar algo, ele deixa a execução por último.
    - Multiplos defer, funcionam como uma pilha, LIFO.
- Funções anônimas, usadas para serem chamadas apenas uma vez, sem necessidade de criação e nome.
    - Podendo ser criadas com invocação imediata ou invocação apenas quando chamada
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

### Métodos
- São funções especificas de um tipo. Podendo ser acessadas apenas por esse tipo, ex:
```go
type pessoa struct {
	name string
}

func (p pessoa) printName() {
	fmt.Print(p.name)
}

func main() {

	pessoa := pessoa{"Test"}

	pessoa.printName()

}
```
- Podemos usar métodos com a intenção de alterar o valor usando ponteiros, ex:
```go
type pessoa struct {
	name string
}

func (p *pessoa) changeName(name string) {
	p.name = name
}

func main() {

	pessoa := pessoa{"Test"}

	pessoa.changeName("novo teste")
}
```

### Ponteiros
- São variáveis que apontam para um endereço de memória.
- Um ponteiro declarado mas não dado o valor(`var a *int`), tem valor **nil**
- Quando queremos passar o endereço de memória de uma variável para um ponteiro, usamos **&**, ex
```go
var a int = 1
var b *int = &a
```
- No exemplo acima, b aponta para o endereço de memória de a, se usarmos `fmt.Println(*b)` teremos o valor **1** como output.
- Quando usado uma variável para apontar para o endereço de memória, para pegar o valor do endereço de memória, usa *, ex:
```go
x := 10
y := &x // & define y com o mesmo endereço de memória de x
fmt.Println(*y) //ira retornar o valor do endereço de memória de y
```
- Ou
```go
x int := 10
y *int := &x // & define y com o mesmo endereço de memória de x
fmt.Println(*y) //ira retornar o valor do endereço de memória de y
```
- Para passar o ponteiro e receber o endereço dentro de uma função, ex:
```go
x := 0
changeNumber(&x)

func changeNumber(number *int) {
    fmt.Println(number) //endereço de memória
    fmt.Println(*number) // valor do numero recebido
    *number++ // acrescenta no valor e não apenas no scopo dentro da função
}
```
- Usamos **(*)** no tipo da variável quando queremos indicar que é um ponteiro do tipo informado.
- Usamos **(*)** na variável quando queremos desferenciar um ponteiro.
- Usamos **(&)** para criar um ponteiro.

### Interfaces
- Funciona como um contrato, semelhante em orientação a object, mas sem a necessidade de implementar diretamente, ex:
```go
type printer interface {
	print()
}

type person struct {
	name string
}

func (p person) print() {
	fmt.Println(p.name)
}

type dog struct {
	name string
}

func (d dog) print() {
	fmt.Println("Au au")
}

func print(p printer) {
	p.print()
}

func main() {
	person := person{"Carlos"}
	print(person)

	dog := dog{"Carlos"}
	print(dog)
}
```

### Goroutines
- Gouroutines é a forma que Go trabalha com concorrencia usando algo similar a threads, mas mais leves.
- Deadlock acontece quando todos os processos estão bloqueados enquanto esperam por eles mesmos, fazendo com que o programa não possa continuar.
- Qualquer função pode se tonar uma goroutine simplesmente usando a palavra chave **go** em frente a função, ex:
```go
func main() {
    go doSomething()
    doSomething2()
}

func doSomething() {
    // do something
}
```

### Canais (channel)
- Canais são uma forma de fazer sincronização em código concorrente.
- Eles nos permitem trasmitir valores entre goroutines.
- A comunicação é semelhante em um cano, tem uma entrada e uma saída. Elas entram e saem na mesma ordem até o channel ser fechado.
- Para adicionar e retirar informação de um channel, precisa ser feito de forma concorrente.
    - Não podendo adicionar e retirar em uma mesma goroutine.
- Para criar um channel, tem duas formas, ex:
```go
func main() {
    var ch chan string //podendo ser de qualquer tipo
    
    ch2 := make(chan int)
}
```
- Canais enviam e recebem dados, usando **<-**, ex:
```go
func main() {
    ch := make(chan string)

    go speak(ch)

    data := <-ch //recebe
    //data vai ter o valor de 'Hello World!'
}

func speak(ch chan string) {
    ch <- "Hello World!" //envia
}
```
- Canais por padrão são bidirecionais, enviam e recebem dados, porém podemos restringir para fazer apenas uma das funções, ex:
```go
func main() {
    ch := make(chan string)

    go speak(ch)

    data := <-ch //recebe
    //data vai ter o valor de 'Hello World!'
}

func speak(ch chan<- string) {
    //chan<- só é possível enviar dados
    ch <- "Hello World!" //envia
}
```
- Quando terminamos de usar um canal, este deve ser fechado, usando `close(ch)`
- Opcionalmente, podemos testar se um canal foi fechado usando um segundo parâmentro como expressão, este parametro indice como um booleano a situação do canal, ex:
```go
func main() {
    ch := make(chan string)

    go speak(ch)

    data, ok := <-ch
    //ok sera falso pois esta aberto neste momento

    close(ch)
}
```
- Um canal quando não é fechado usando `close(channel)`, pode ocorrer o deadlock, que seria quando um canal parou de enviar informação, mas alguém ainda está ouvindo e esperando por algo a ser enviado.
- Exemplo deadlock:
```go
func main() {
    channel := make(chan int)

    go loop(channel)

    for {
        number := <-channel
        fmt.Println(number)
    }
    //resultado:
    // 0
    // 1
    // 2
    // 3
    // 4
    // fatal error: all goroutines are asleep - deadlock!
    //devido ao loop infinito, apos printar os 5 numeros, continuará esperando, gerando o deadlock
}

func loop(channel chan int) {
    for i := 0; i < 5; i++ {
        channel<- i
    }
}
```
- Para corrigir e não acontecer o deadlock, pode ser verificado se o channel ainda está aberto e fechar quando ele não ser mais necessário
- Exemplo correção deadlock:
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
    //fecha o channel apos finalizar a enviar os numeros
    close(channel)
}
```

### Testes
- Para criar testes, o Go disponibiliza ferramentas nativas nos seus pacotes
- Para rodar os testes, pode ser feito no pacote que contem os testes, `go test`
- Para rodar todos os testes do projeto, usar `go test ./...`
- Para rodar com o modo verboso, `go test -v`
- Para rodar com a cobertura de testes, `go test --cover`
- Tem um modo que gera um txt com a cobertura de cada pacote. Esse arquivo é gerado e feito a leitura por outro comando Go.
    - Para gerar o arquivo, `go test --coverprofile NOME_ARQUIVO.txt`
    - Para visualizar a cobertura por cada pacote no terminal, `go tool cover --func=NOME_ARQUIVO.txt`
    - Para visualizar a cobertura por cada pacote em html, `go tool cover --html=NOME_ARQUIVO.txt`
- Cada teste deve ter o seguinte formato:
    - Criar o arquivo .go com o respectivo nome _test.go
        - ex: Para o main.go, criar o main_test.go no mesmo pacote
    - Cada teste deve começar com Test antes do nome do método e adicionar o parametro para uso das validacoes
        - ex: TestMetodoXpto(t *testing.T)
    
### Packages
- O pacote main é o principal como o nome já diz. Podendo ser utilizado com varios arquivos .go neste mesmo pacote, a diferença está na forma de rodar, os arquivos precisam ser declarados no `go run main.go xxx.go yyy.go` ou na raiz `go run .`.
- Novos pacotes podem ser criado com outras pastas com o nome do pacote.
- Para fazer o import de funções ou variáveis de um pacote diferente, basta declarar o nome da função como pascal case.
- Package management
    - `go get <LIB>` baixa e faz o build do código
    - `go get -u <LIB>` baixa o código da lib atualizado, caso houver
    - `go intall <LIB>` faz a compilação da lib

### Modulos
- Modulos servem para gerenciamento de dependências em projetos Go
- Modulos são coleções de pacotes indicados dentro do **go.mod**
- `go mod init <MOD_NAME>` cria um novo modulo
- `go mod tidy` remove/adiciona dependências em **go.mod**

### Workspaces
- Nos permitem trabalhar com multiplos modulos simultaneamente.
- Funciona de forma similar a modulos.
- Ajudam para rodar um projeto local com alterações de um módulo dependente. Quando temos um projeto x, que usa o modulo y, porém fizemos alterações no módulo y e ele n está com estas alterações no repositório remoto.
- Para criar um workspace, criar uma pasta que será utilizada como workspace, inicializar o workspace com `go work init`
- Para adicionar os modulos dentro do workspace, utilizar `go work use ./<MODULE>`
- Após feito isso, o modulo será inserido no workspace, os modulos que dependem de outro podem ser executado normalmente com as alterações que foram feitas locais.
- Um arquivo contendo os modulos e o workspace será criado após rodar `go work init`, com o nome go.work, ex:
```go
go 1.18

use(
    ./module1
    ./module2
)
```
- Podem ser criados *workspaces* de forma geral e adicionar uma variável de ambiente, cada *módulo* adicioná-lo ao *workspace*. Para fazer isso,
adicionar *GOWORK* como variável do sistema e indicar o path da pasta. Para verificar o local do *GOWORK, usar `go env GOWORK` no terminal.

### Erros
- No Go não temos exceções e sim erros, e dessa forma, os erros são tratados de forma diferente.
- Podendo usar o pacotes errors para criar seus erros a partir de `errors.New("Deu erro")`
- Exemplo usando divisão por 0:
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
- Outra forma de customizar o erros, seria utilizando `fmt.Errorf("cannot divide %d by 0", a)`
- Existe dentro de Go, **panic** e **recover** que são interfaces internas similares ao **try catch** conhecido em outras linguagens.