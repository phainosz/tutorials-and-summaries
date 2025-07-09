# Anotações gerais sobre Markdown

- [Comandos gerais](#comandos-gerais)
- [Cabeçalho](#cabeçalho)
- [Ênfase](#ênfase)
- [Listas](#listas)
- [Links](#links)
- [Quotes](#quotes)
- [Tarefas](#tarefas)
- [Código](#código)
- [Detalhes](#detalhes)

## Comandos gerais

- Para criar um arquivo md, basta criar o arquivo com extensão .md

## Cabeçalho

- Semelhante ao html, o uso de # serve para criação de headers
- 1 # é semelhante ao \<h1\> pode chegar até 6 #

## Ênfase

- Para destacar texto com negrito, itálico ou riscado
- Usar 2 **asteriscos** ou 2 __underlines__ para alterar o texto em negrito
- Usar 1 *asterisco* ou 1 _underline_ para alterar o texto em itálico
- Usar \<del\>\</del\> para alterar o texto riscado
- Usar \<s\>\</s\> para alterar o texto riscado

## Listas

- Usar - ou * ou + para listas

## Links

- Para criar links, usar \[\<NAME>\]\(\<LINK>\)
    - Ex: [inicio](#comandos-gerais)

## Quotes

- Para criar quotes, usar >
  > Ex: criando quote

## Tarefas

- Podem ser criadas tasks com ou sem done
- Ex:

    - [x] Tarefa 1
    - [x] Tarefa 2
    - [ ] Tarefa 3

## Código

- Usado para fazer o uso real de códigos, usar 1 ` ou 3 ```
- Pode utilizar o nome da linguagem ao final dos 3 `, ```go
- Ex:

```go
func main() {
    
}
```

## Detalhes

- Usado para mostrar/esconder conteúdos.
- Ex:

<details>
  <summary>Click me</summary>

### Heading

1. Foo
2. Bar
    * Baz
    * Qux

</details>