# Anotaçẽs gerais sobre Python

- [Instalação](#instalação)
- [Geral](#geral)
- [Condicionais](#condicionais)
- [Loops](#loops)
- [Funções](#funções)
- [Listas](#listas)
- [Tuplas](#tuplas)
- [Dicionários](#dicionários)
- [Sets](#sets)
- [Exceções](#exceções)
- [Módulos](#modulos)
- [OOP](#oop)
- [Testes](#testes)

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
    print(f"My age is {age}") # print My age is 18
    ```
  - Podendo ser usado de outra forma, mostrar o valor da variável e seu nome:
    ```python
    age = 18
    print(f"{age=}") # print age=18
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
- Quando temos algum recurso que é necessário chamar a *função* `close()`, podemos usar o **with** para fazer isso de forma automática.
  - Exemplo sem `with`:
    ```python
    f = open('file.txt')
    print(f.read())
    f.close()
    ```
  - Exemplo com `with`:
    ```python
    with open('file.txt') as f:
      print(f.read())
    ```

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
- Podemos usar atribuições de variáveis com seu tipo, isso é chamado de *type annotations*. Basicamente serve de documentação para o desenvolvedor, não irá afetar na interpretação do código.
  - Ex:
    ```python
    age: int = 18
    text: str = "hello world"
    price: float = 1.99
    active: bool = False

    def greet(name: str) -> None: # use None to represent no return in a function
      print(f"Hello {name}")

    ```

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
    ```

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
- Em **python** podemos usar *funções lambdas* para criar *funções* sem uma declaração. Ex:
  ```python
  # lambda parameter: expression
  square = lambda x: x ** 2
  print(square(4)) # print 16
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
- Podemos fazer o *slice* de uma *lista* seguindo a seguinte sintaxe: `list[begin: end: step]`.
  - *begin* tem o valor padrão 0.
  - *end* tem como valor padrão o tamanho da lista.
  - *step* tem o valor padrão 1.
  - Todos os valores passados, precisam ser índices válidos.
  - *Slice* retorna uma nova lista.
  ```python
  colors = ['red', 'orange', 'yellow', 'green', 'blue', 'indigo', 'violet']
  example_1 = colors[1:4]
  print(example_1) # prints ['orange', 'yellow', 'green']

  example_2 = colors[:3]
  print(example_2) # prints ["red", 'orange', 'yellow']

  example_3 = colors[-1:]
  print(example_3) # prints ['violet']

  example_4 = colors[::2]
  print(example_4) # prints ['red', 'yellow', 'blue', 'violet']

  example_5 = colors[::-1]
  print(example_5) # prints reversed list ['violet', 'indigo', 'blue', 'green', 'yellow', 'orange', 'red']
  ```
- Podemos acessar valores de uma lista de uma forma diferente. Ex:
  ```python
  colors = ['red', 'blue', 'green']
  red, blue, green = colors
  print(red) # prints red
  print(blue) # prints blue
  print(green) # prints green

  red, blue = colors # ValueErros: too many values to unpack

  red, *others = colors
  print(red) # prints red
  print(others) # prints ['blue', 'green']
  ```
- Para fazer um loop em uma lista, podemos fazer da seguinte maneira:
  ```python
  cities = ['New York', 'Beijing', 'Cairo', 'Mumbai', 'Mexico']

  for city in cities:
    print(city)

  # if we want to know the index, use enumerate
  for item in enumerate(cities):
    print(item) # print (index, item) = (0, 'New York')...

  for index, city in enumerate(cities):
    print(f"{index}: {city}")
  ```
- Para encontrar um *index* em uma *lista* temos duas formas. Ex:
  ```python
  cities = ['New York', 'Beijing', 'Cairo', 'Mumbai', 'Mexico']

  result = cities.index("Cairo")
  print(result) # print 2

  # if element doen't exist
  result = cities.index("Osaka")
  # ValueError: 'Osaka' is not in list

  city = 'Osaka'
  if city in cities:
    print(cities.index(city))
  else:
    print(f"{city} doesn't exist in the list")
  ```
  - Em programação, geralmente precisamos alterar os valores de cada elemento de uma lista e retonar uma nova. **List comprehension* permite fazer isso de uma forma simplificada.
    - Ex:
      ```python
      number = [1, 2, 3, 4, 5]

      squares = []
      for number in numbers:
        squares.append(number**2)

      print(squares) # print [1, 4, 9, 16, 25]

      # map
      squares = list(map(lambda number: number ** 2, numbers)) # map() returns an interator. list() transform the interator to a list
      print(squares) # print [1, 4, 9, 16, 25]

      # list comprehension
        # syntax [output_expression for element in list]
      squares = [number**2 for number in numbers]
      print(squares) # print [1, 4, 9, 16, 25]

      # filter
      filtered_list = list(filter(lambda number: number > 3, numbers)) # map() returns an interator. list() transform the interator to a list
      print(filtered_list) # print [4, 5]

      # list comprehension with if condition
        # syntax [output_expression for element in list if condition]
      filtered_list = [number for number in numbers if number > 3]
      print(filtered_list) # print [4, 5]
      ```

## Tuplas
- Uma **tupla** pode ser considerada uma *lista imútavel*.
- Para criar uma *tupla* usar: `my_tuple =  (1,2,3)`.
- Ex:
  ```python
  coordinates = (123, 456)
  print(coordinates[0]) # prints 123
  print(coordinates[1]) # prints 456

  # or
  x, y = coordinates
  print(x) # prints 123
  print(y) # prints 456
  ```

## Dicionários
- Em **python** um *dicionário* é uma coleção no fomato *chave-valor*.
- A *chave* deve ser um valor *imutável*.
- A declaração de um *dicionário* é a seguinte: `empty_dict = {}`.
- Para atribuir valores em inicialização, Ex:
  ```python
  person = {
    'first_name': 'John',
    'last_name': 'Doe',
    'age': 25,
    'active': True
  }

  # access values
  print(person['first_name'])
  # or
  print(person.get('first_name'))

  # add values
  person['gender'] = 'Male'

  # change values
  person['age'] = 30

  # remove keys
  del person['active']

  # loop dictionary
  for key, value in person.items():
    print(f"{key}: {value}")

  # loop dictionary keys
  for key in person.keys():
    print(key)

  # loop dictionary values
  for value in person.values():
    print(value)
  ```
- Assim como em **lista** temos *list comprehension*, em **dicionários** temos *dictionary comprehension*.
  - Funciona de forma semelhante. Ex:
    ```python
    my_dict = {
        'A': 1,
        'B': 2,
        'C': 3,
        'D': 4,
    }

    new_dict = {}
    for key, value in my_dict.items():
        new_dict[key] = value*2

    print(new_dict) # print {'A': 2, 'B': 3, 'C': 4, 'D': 5}

    # dict comprehension
    new_dict = {key: value * 2 for (key, value) in my_dict.values()}
    print(new_dict) # print {'A': 2, 'B': 3, 'C': 4, 'D': 5}

    # dict comprehension with filter
    new_dict = {key: value * 2 for (key, value) in my_dict.values() if value > 2}
    print(new_dict) # print {'C': 4, 'D': 5}
    ```

## Sets
- São coleções de dados que não possuem *ordenação* dos elementos, não aceitas *itens duplicados*.
- Para defirnir um **set**, usar: `empty_set = set()`.
- Não confundir com **dicionarios**, pois para criar um **set** preenchido, usa-se o seguinte: `my_set = {'Python', 'Java', 'Golang'}`.
- Podemos usar **set comprehension**, funciona da mesma forma que em **lista**, basta trocar **[]** por **{}**.
  - Podemos usar uma lista como *coleção* de entrada. O **set** gerado irá remover elementos duplicados e aplicar o **set comprehension**.
    ```python
    numbers = [1, 2, 3, 4, 5]

    squares = {number ** 2 for number in numbers}
    print(squares) # print {2, 4, 9, ,16, 25}
    ```

## Exceções
- Em **python** temos dois tipos de *erros*, erros de *sintaxe* e *exceções*.
  - Errors de *sintaxe* pode ser por falta de **:** em um *if*, identação incorreta, etc.
  - *Exceções* ocorrem durante execução do código, podem ser por diversos motivos, conversões incorretas, acessar algo que não existe, etc.
- A sintaxe em **python** é a seguinte:
  ```python
  number = int(input('Type a number: ')) # digit letter instead
  # if pressed a leeter instead a number, ValueError exception will occur

  print(in)

  try:
    number = int(input('Type a number: '))

    print(number)
  except:
    print('Error! Please enter a valid number')
  ```
- Podemos informar que tipo de *exceção* queremos capturar, agrupar *exceções* que queremos ter o mesmo tratamento. Ex:
  ```python
  try:
    number = int(input('Type a number: '))

    result = 10 / number # if number is 0, exception ZeroDivisionError will occur

    print(number)
  except ValueError:
    print('Error! Please enter a valid number')
  except ZeroDivisionError:
    print('Error! Number is 0')

  # or
  try:
    number = int(input('Type a number: '))

    result = 10 / number # if number is 0, exception ZeroDivisionError will occur

    print(number)
  except (ValueError, ZeroDivisionError):
    print('Error! Please enter a valid number')
  ```
- Existem casos que queremos que algo sempre seja executado, independente de *exception* ou não, nesses casos usamos a cláusula *finally*. Ex:
  ```python
  a = 10
  b = 0

  try:
    c = a / b
    print(c)
  except ZeroDivisionError as error:
    print(error)
  finally:
    print('Finishing up.')

  # we can use try ... finally withou the except statement
  try:
    c = a / b
    print(c)
  finally:
    print('Finishing up.')
  ```
- Para criar uma **exceão** usar a **keyword** **raise**. Ex:
  ```python
  name = input('Enter your name: ')

  if not name:
    raise ValueError('Invalid name') # raise exception when name is blank
  else:
    print(name)
  ```

## Modulos
- Um módulo é uma parte do código com uma funcionalidade especifica.
- Em **pyton** um módulo é um arquivo que contains código python.
- A nomenclatura do módulo, será o nome do arquivo sem o `.py` ao final. Ex:
  ```python
  # pricing.py

  def get_net_price(price, tax_rate, discount=0):
    return price * (1 + tax_rate) * (1-discount)


  def get_tax(price, tax_rate=0):
    return price * tax_rate
  ```

  ```python
  # main.py
  import pricing

  net_price = pricing.get_net_price(price=100, tax_rate=0.01)
  print(net_price)

  # or
  from princing import get_net_price
  net_price = get_net_price(price=100, tax_rate=0.01)
  print(net_price)
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
- Em **python** para criar uma classe usamos a seguinte sintaxe:
  ```python
  class Person:
    pass # pass is used to allow the class to have an empty body, Withou pass, the interpreter would raise IndentationError

  person = Person()

  # check object is instance of specific class
  print(isinstance(person, Person))
  ```
- Por ser uma linguagem dinâmica, podemos adicionar atributos em uma instância de uma classe, porém estes atributos somes em uma nova instância.
- Para definir um instanciador de classe, usar o método `__init__`:
  ```python
  class Person:
    # self is the instance of the class
    def __init__(self, name, age):
      self.name = name
      self.age = age

  person = Person('John', 25)
  ```
- Podemos criar *funções* para uma classe, chamados de *métodos*:
  ```python
  class Person:
    def __init__(self, name, age):
      self.name = name
      self.age = age

    def greet(self):
      return f"Hi, it's {self.name}"

  person = Person('John', 25)
  print(person.greet())
  ```
- Podemos definir *atributos* para uma classe, estes atributos são compartilhados entre as instâncias da classe:
  ```python
  class Person:
    counter = 0

    def __init__(self, name, age):
      self.name = name
      self.age = age

    def greet(self):
      return f"Hi, it's {self.name}"

  person = Person('John', 25)
  print(person.greet())
  person.counter

  # or from a class
  Person.counter
  ```
- Podemos criar *métodos* de uma classe que podem ser compartilhadas por todas as instâncias, assim como *atributos*:
  ```python
  class Person:
    def __init__(self, name, age):
      self.name = name
      self.age = age

    @classmethod # it's a decorator to make a class method, allow access to class attributes
    def create(cls): # need first argument. cls is the class itself. cls is a convention name.
      return Person('Doe', 22)

  person = Person.create()
  print(person)
  ```
- Podemos criar *métodos* de uma classe, que não fazem acesso aos dados da instância:
  ```python
  class TemperatureConverter:
    @staticmethod
    def celsius_to_fahrenheit(c):
      return 9 * c / 5 + 32

    @staticmethod # it's a decorator to make methods that doesn't have access to class state.
    def fahrenheit_to_celsius(f):
      return 5 * (f - 32) / 9

  fahrenheit = TemperatureConverter.celsius_to_fahrenheit(30)
  print(fahrenheit) # print 86
  ```
- **Herança** é feita da seguinte forma:
  ```python
  class Employee(Person):
    def __init__(self, name, age, job_title):
      super().__init__(name, age)
      self.job_title = job_title

  employee = Employee('John', 25, 'Developer')
  ```
- Em **python** não temos o conceito de *atributos* privados, para definir que um atributo é privado, usados **_** para informar que o *atributo* será privado.
  ```python
  class Counter:
    def __init__(self):
      self._current = 0

    def increment(self):
      self._current += 1

  counter = Counter()
  counter.increment()
  ```
- Em **python** podemos criar *properties** e com isso alterar **getter** e **setter**.
  ```python
  class Person:
    def __init__(self, age):
      self.age = age

    @property # create a getter for the attribute
    def age(self):
      return self._age

    @age.setter
    def age(self, age):
      if age <= 0:
        raise ValueError('Invalid age')
      self._age = age

  person = Person(10)
  print(person.age) # print 10

  person.age = 0 # will raise exception
  person = Person(0) # will raise exception
  ```
- **Python** possui **enums** e são criados da seguinte forma:
  ```python
  from enum import Enum

  class Color(Enum):
    RED = 1
    GREEN = 2
    BLUE = 3

  print(Color.RED.name) # print RED
  print(Color.RED.value) # print 1
  ```

## Testes
- Testes pode ser feitos de várias formas, será abordado testes *unitários* nesse momento.
- **Testes unitários** verificam um pedaço de código como uma unidade.
- Usado para verificar se este pedaço está fazendo o que foi programado para fazer.
- **Python** possui um módulo nativo para isso, `unittest`.
  ```python
  #square.py
  class Square:
    def __init__(self, legnth) -> None:
      if type(length) not in [int, float]:
        raise TypeError('Length must be a number')
      self.length = length

    def area(self):
      return self.length * self.length
  ```
  ```python
  # test_square.py
  import unittest

  from square import Square

  class TestSquare(unittest.TestCase):
    def test_area(self):
      square = Square(10)
      are = square.area()
      self.assertEqual(area, 100)

    def test_length_with_wront_type(self):
      with self.assertRaises(TypeError)
        square = Square('10')

  # run test with python test_square.py
  # remove this and run python -m unittest to run without this if block.
  if __name__ == '__main__':
    unittest.main()
  ```
- Existem casos em que queremos que algo rode antes ou após os testes, exemplo:
  ```python
  import unittest

  def setUpModule():
    print('Running setUpModule')


  def tearDownModule():
    print('Running tearDownModule')


  class TestMyModule(unittest.TestCase):
    @classmethod
    def setUpClass(cls):
      print('Running setUpClass')

    @classmethod
    def tearDownClass(cls):
      print('Running tearDownClass')

    def setUp(self):
      print('')
      print('Running setUp')

    def tearDown(self):
      print('Running tearDown')

    def test_case_1(self):
      self.assertEqual(5+5, 10)

    def test_case_2(self):
      self.assertEqual(1+1, 2)

  # the output running with python -m unittest -v
  #Running setUpModule
  #Running setUpClass
  #test_case_1 (test_my_module.TestMyModule) ...
  #Running setUp
  #Running test_case_1
  #Running tearDown
  #ok
  #test_case_2 (test_my_module.TestMyModule) ...
  #Running setUp
  #Running test_case_2
  #Running tearDown
  #ok
  #Running tearDownClass
  #Running tearDownModule
  #
  #----------------------------------------------------------------------
  #Ran 2 tests in 0.002s
  #
  #OK
  ```
- Podemos usar `@unittest.skip('Work in progress')` em *métodos* e *classes* para pular o teste.
  - Além de pular testes, há a possibilidade de pular testes com condições:
    - `@unittest.skipIf(condition, reason)`.
      - Pular testes no windows: `@unittest.skipIf(platform.startswith("win"), "Do not run on Windows")`.
    - `@unittest.skipUnless(condition, reason)`, pula o teste se a condição não for verdadeira.
- Existem casos em que não queremos usar o valor real ou não temos como usar um valor especifico no *teste*, para isso usamos **mock**:
  ```python
  # odometer.py
  from random import randint
  def speed():
    return randint(40, 120)

  def alert():
    speed = speed()
    if speed < 60 or speed > 100:
      return True
    return False
  ```

  ```python
  # odometer_test.py
  import unittest
  from unittest.mock import Mock
  import odometer

  class TestOdometer(unittest.TestCase);
    def test_alert_normal(self):
      odometer.speed() = Mock() # mock function speed()
      odometer.speed.return_value = 70 # every speed() call, return value 70
      self.assertFalse(odometer.alert())

    def test_alert_overspeed(self):
      odometer.speed() = Mock() # mock function speed()
      odometer.speed.return_value = 100 # every speed() call, return value 100
      self.assertFalse(odometer.alert())

    def test_alert_underspeed(self):
      odometer.speed() = Mock() # mock function speed()
      odometer.speed.return_value = 59 # every speed() call, return value 59
      self.assertFalse(odometer.alert())

  # run the test python -m unittest test_odometer.py -v
  ```
- Podemos verificar a cobertura dos testes, o que foi testado e o que faltou testar.
  - Para isso, precisamos adicionar o módulo *coverage*: `pip install coverage`.
  - Para rodar o teste verificando a cobertura, seguir duas etapas, rodar o teste e verificar a cobertura do arquivo gerado.
    - `python -m coverage run -m unittest` irá gerar o arquivo de *report*.
    - `python -m coverage report` irá mostrar como ficou a cobertura do código testado.