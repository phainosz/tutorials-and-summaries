# Anotaçẽs gerais sobre Python

- [Instalação](#instalação)
- [Geral](#geral)
- [Condicionais](#condicionais)
- [Loops](#loops)
- [Funções](#funcoes)

## Instalação
- [Link site oficial](https://www.python.org/downloads/)
- `python --version` para ver a versão instalada.

## Geral
- **Python** é uma linguagem de programação interpretada.
- **Python** possui um *REPL(read-eval-print loop)* que possibilita interagir com a linguagem via terminal. Insira o comando `python` no terminal que irá entrar nesse modo.
  - Para sair, usar o comando `exit()`.
- *Strings* podem ser escritas com **'** ou **"**, podendo ser usada **"""* para um texto com várias linhas.
- Formatar uma *string* em **python** é feito da seguinte forma:
  - Ex:
  ```python
  age = 18
  print(f"My age is {age}")
  #print My age is 18
  ```
  - Podendo ser usado de outra forma, mostrar o valor da variável e seu nome:
  ```python
  age = 18
  print(f"{age=}")
  #print age=18
  ```
- Para executar um arquivo **python**, usar `python file.py`.
- **Python** não faz o uso de **;**.
- **Python** usa *identação* e *espaços* para estruturar código.
- Operadores condicionais são usados para comparar um valor com outro. Para isso temos alguns tipos de operadores:
  - *Menor que(<)*: `1 < 2` -> verdadeiro
  - *Maior que(<)*: `1 > 2` -> falso
  - *Menor igual que(<=)*: `1 <= 2` -> verdadeiro
  - *Maior igual que(<)*: `1 >= 2` -> falso
  - *Igual(==)*: `1 == 2` -> falso
  - *Diferente(!=)*: `1 != 2` -> verdadeiro
  - Operadores lógicos são usados para comparar valores e tomar decisão baseados em condições.
    - *and*: `1 == 1 and 2 > 1` -> verdadeiro
    - *or*: `1 == 1 or 2 > 1` -> verdadeiro
    - *not*: `not 1 < 2` -> falso
- **Jupyter Notebook**

## Variáveis
- Em **python** basta nomear a variável e escolher qual o tipo será assinalado para ela: `my_var = 10`.
- Usar padrão *snake_case* para variáveis.
- Os **tipos de dados** para variáveis mais comuns são:
  - *str* para string e character.
  - *int* para números inteiros.
  - *float* para números decimais.
  - *bool* para valores booleanos.
- Para checar o tipo da variável, podemos usar a *função* `type`: `type("what type is this")`.

## Condicionais
- Usados para controle condicional usando uma *variável* ou um valor específico como base.
  - Ex:
  ```python
  age = 18
  if age < 18:
    print("Under 18")
  elif age == 18:
    print("Is 18")
  else:
    print("Above 18")

## Loops
- Em programação, **loops** são essenciais para percorrer uma estrutura de dados, repetir uma sequência de código até uma condição específica.
- Em **Python** temos 2 tipos de **loops**: `for` e `while`.
  Ex `for`:
  ```python
  for i in range(5): # iterates from 0 to 4
    print(i)
  ```
  Ex `while`:
  ```python
  i = 0
  while i < 5:
    print(i)
    i += 1
  ```
- Podemos usar o `break` em casos onde queremos parar o *loop* devido à uma condição.
  - Ex:
  ```python
  for i in range(5):
    if i == 3:
      break
    print(i)
  ```
- Podemos usar o `continue` em casos onde queremos pular um passo do *loop* devido à uma condição.
  - Ex:
  ```python
  for i in range(10):
    if i % 2 == 0:
      continue
    print(i) # print only odd numbers(1,3,5,7,9)
  ```

## Funções
- **Funções** são blocos de códigos reutilizáveis, que realizam tarefas específicas, podendo retornar valores ou não.
- Em **python** usamos a palavra chave **def** para definir uma *função*.
  - Ex:
  ```python
  def greet(name):
    return f"Hello {name}"

  print(greet("John"))
  ```
- Podendo ser adicionado uma documentação sobre a função e seus parâmetros.
  - A primeira linha após uma **função**, sendo ela uma string, é interpretada como **docstring**.
  - Para ver a **docstring** de um **função** usar a **função** `help()`, com a função que deseja ver a doc: `help(print)`.
  - Ex:
  ```python
  def greet(name):
    """
    Returns a personalized greeting for the given name.

    Args:
        name (str): The name of the person to greet.

    Returns:
        str: A greeting message in the format "Hello {name}".
    """
    return f"Heelo {name}"

  print(greet("John"))
  ```
- Podemos criar valores padrôes para parâmetros usados em funções.
  - Ex:
  ```python
  def greet(name, message='Hi '):
    return f"{message} {name}"

  print(greet("John"))
  ```
- Podemos usar argumentos nomeados em casos onde queremos fornecer apenas alguns valores para a **função** chamada.
  Ex:
  ```python
  def get_price(price, discount):
    return price * (1 - discount)

  print(get_price(100, 0.1))

  # if we want a default value for discount, we modify to this
  def get_price(price, discount=0.1):
    return price * (1 - discount)

  # and use it like that
  print(get_price(100))

  # but what if we had another paramter called tax with a default value and we wanted to modify only discount value?
  def get_price(price, tax=0.07, discount=0.05):
    return price * (1 + tax - discount)

  print(get_price(100)) # its ok
  print(get_price(100, 0.06)) # it would only modify tax to 0.06 and not discount
  print(get_price(price=100, discount=0.06)) # that would work
  print(get_price(price=100, discount=0.06, 0.08)) # that would cause an error
  ```
- Podemos usar argumentos flexíveis em uma *função*.
  - Ex:
  ```python
  def print_args(*args):
    for arg in args:
      print(arg)

  print_args(1,2,3,4) # internally *args is treated as a tuple
  ```

## Listas
- Uma lista é uma coleção de itens.
- Em **python** usa-se **[]** para indicar uma *lista*. Ex: `my_list = []`.
- Para acessar um item de uma lista, usar `list[index]`.
  - `list[0]` irá acessar o primeiro item da *lista*.
  - `list[-1]` irá acessar o último item da *lista*.
- Para modificar um elemento da *lista*, segue o mesmo que acessar o elemento. Ex: `list[0] = 10`.
- Para adicionar mais item na lista, podemos usar
  - `list.append(item)`, adiciona o item ao fim da lista.
  - `list.insert(item, index)`, adiciona o item no índice informado.
- Para remover itens da *lista*, usar:
  - `del list[0]`. remove o item informado através do índice.
  - `list.remove(0)`. remove o item informado através do índice.
