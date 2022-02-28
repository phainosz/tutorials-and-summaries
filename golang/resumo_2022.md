# Anotaçẽs gerais sobre Golang


## Instalação
[Golang](https://go.dev/doc/install)

### Primeiros passos
- Criar o arquivo main.go
- Criar o módulo para a aplicação: `go mod init MODULE_NAME`
- Adicionar o pacote: `package main`
- Criar a função principal: `func main()`
- Como rodar: `go run main.go`

### Variáveis
- var, const
- tipos int, int8, uint, string, float ...
- Inferência usando := ex: `name := "Paulo`
- Operações em tipos numéricos devem ser do mesmo tipo

### Ponteiros
- Usar & para apontar para o local em memória de uma variável
- Exemplo de uso, ponteiro para adicionar valor em variável usando Scan: `fmt.Scan(&myVar)`

### Arrays
- Sintaxe: `var array = [50]string{}` ou `var array [50]string`
- Para adicionar, é da mesma forma convencional: `array[0] = "String"`
- Tamanho total do array ex: `len(array)`

### Slices
- É uma abstração do array com tamanho dinâmico
- Criado igual o array mas sem o tamanho do array, ex: `var slice[]string` ou `var slice = []string{}`
- Para adicionar no próximo elemento do slice, é utilizado append, ex: `slice = append(slice, "Dado")`

### Maps
- É uma collection de chave valor
- Criado usando chave e valor tipados, ex: `var mymap map[string]string` ou um map vazio `var mymap = make(map[string]string)`
- Para adicionar no map, é utilizado append, ex: `mymap["key"] = value`


### Loops
- Apenas for existe no Go, while, doWhile não existem
- O mesmo de C ou Java, ex: 
```
sum := 0
for i := 1; i < 5; i++ {
    sum += i
}
```
- Maneira que se assemelha ao whie, ex: 
```
n := 1
for n < 5 {
    n *= 2
}
```
- Loop infinito, ex:
```
sum := 0
for {
    sum++ 
}
```
- ForEach range loop, ex:
```
strings := []string{"hello", "world"}
for index, element := range strings {
    fmt.Println(i, s)
}
```
- Em casos onde o index do ForEach não é necessário, pode utilizar _ para ignorar o indice, ex:
```
strings := []string{"hello", "world"}
for _, element := range strings {
    fmt.Println(i, s)
}
```
### Condições IFs e Switch
- Seguem o mesmo formato, apenas muda o fato de usar () após o if, ex:
```
if someVariable {

} else {

}
```
- Para o switch, mesma coisa, ex:
```
switch someVariable {
    case 1:
        //do something
    case 2, 3, 4:
        //do something
    default:
        //do default
}
```
### Funções
- A nomenclatura usada no Go é func.
- Funções sem retorno, ex:
```
func someFunction() {
    //do something
}
```
- Funções com retorno, ex:
```
func someFunction() string {
    //do something
    return someString
}
```
- No Golang, pode ser retornado múltiplos valores, ex:
```
func someFunction() (string, int) {
    //do something
    return someString, someInt
}
```

### Packages
- O pacote main é o principal como o nome já diz. Podendo ser utilizado com varios arquivos .go neste mesmo pacote, a diferença está na forma de rodar, os arquivos precisam ser declarados no `go run main.go xxx.go yyy.go` ou na raiz `go run .`.
- Novos pacotes podem ser criado com outras pastas com o nome do pacote.
- Para fazer o import de uma função ou variáveis de um pacote diferente, basta declarar o nome da função como pascal case.

### Structs
- Funciona de forma semelhante do C
- Usado como forma de definir multiplos tipos de dados
- Alternativa para classes em Go
- Os campos da struct seguem o padrão de nomenclatura para export de dados, pascal case para usar fora do pacote.
- Ex: 
```
type UserData struct {
	firstName       string
	lastName        string
	email           string
	numberOfTickets uint
}
```
- Como adicionar valores para struct. Primeiro segue como o nome do campo da struct, segundo como o valor, ex:
```
var userData = UserData {
		firstName:       firstName,
		lastName:        lastName,
		email:           email,
		numberOfTickets: userTickets,
	}
```
- Ou de forma simplificada
```
var userData = UserData {
		firstName,
		lastName,
		email,
		userTickets,
	}
```
- Ou adicionar apenas no campo como se fosse um set
```
var userData = UserData{}
	userData.email = "email"
	userData.firstName = "Name"
```