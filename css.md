# Anotaçẽs gerais sobre CSS

- [O que é CSS](#o-que-é-css)
- [Geral](#geral)
- [Seletores](#seletores)

## O que é css
- **CSS** é uma linguagem para estilização da página web.
- **CSS** significa *Cascading Syle Sheets*.
- Com o **css** conseguimos alterar o comportamento do **html**.
- Podemos aplicar **css** de três formar no **html**:
  - *em linha* é aplicado diretamente no *elemento* **html** e assim se torna o prioritário em questão de qual *estilo* será processado.
  - *interno* é definido na *tag* *head* do **html**, dentro do *head* insere-se um *elemento* `<style>`.
  - *externo* é definido separadamente em um outro arquivo, para importar o **css** *externo*, adicionar uma *tag* `<link>` com a referência do arquivo.
    <details>
      <summary>Ex:</summary>

      ```html
      <!DOCTYPE html>
      <html>

      <head>
        <title>CSS Tutorial</title>
        <!-- Internal CSS -->
        <style>
            span{
                color: green;
            }
        </style>
        <!-- External CSS -->
        <link rel="stylesheet" href="/css/style.css">

      </head>

      <body>
        <h1><span>Tutorials</span>point</h1>
        
        <!-- Inline CSS -->
        <p style="font-weight: bold; 
                  margin-top: -15px; 
                  padding-left: 5px">
            Simple & Easy <span>Learning</span>
        </p>
      </body>

      </html>
      ```
    </details>
- **CSS** possui medidas usadas para determinar dimensões e tamanhos de elementos em página. Temos medidas absolutas como *pixel(px)*, *porcentagem(%)* e *polegadas(in)* e medidas relativas como *em*, *vh*, *vw* e *rem*.
  - *em* é relativa ao tamanho de fonte do elemento.
  - *vh* é relativo à altura, 1vh equivale à 1%.
  - *vw* é relativo à largura, 1vw equivale à 1%.
  - *rem* é relativa ao tamanho de fonte do elemento raiz.

## Geral
- *box model* é usado para falar de layout e design, consiste em *conteúdo*, *padding*, *border* e *margin* nesta ordem, como um caixa onde o *conteúdo* é o mais interno e *margin* o mais externo.
- `margin: 2px 2px 2px 2px;` usado para manipular espaço ao redor de elementos. Os valores seguem o sentido cima, direita, baixo e esquerda.
- `padding: 2px 2px 2px 2px;` usado para manipular espaço dentro dos elementos. Os valores seguem o sentido cima, direita, baixo e esquerda.
- `background-color: white;` para alterar a cor de fundo.
- `color: green;` para alterar a cor do texto. Podendo usar outros formatos de cor, *hexadecimal*, *rgb*.
- `border: 2px solid blue;` para adicionar borda, com tamano, formato e cor.
  - `border` pode ser *solid(solida)*, *dotted(pontilhada)*, *dashed(tracejada)* entre outras.
- `border-radius: 5px;` adiciona arredodanmento ao elemento.
- `font-family: Arial, Cursive;` usado para definir a fonte do elemento.
- `font-size: 20px;` define o tamanho da fonte do elemento.
- `text-align: left | right | center | justify;` usado para alinhamento do texto.
- `direction: rtl | ltr;` direcionamento do texto.
- `text-transofrm: capitalize | lowecase | uppercase | none;` serve para alterar o *case* do texto.
- `letter-spacing: normal | 5px | -1px;` serve para adicionar espaçamento.
- `height: 10px;` altera a altura.
- `width: 20px;` altera a largura.
- `opacity: 40%;` altera a opacidade do elemento.
- `position: static(default) | relative | absolute | fixed | sticky;` define como o elemento é posicinado na página web, controla como o elemento será posicionado em relação ao local inserido, seja ele dentro de outro container ou no próprio *body*. Para configurar as posições, usar *top, left, right, bottom*.
  - *static* é o valor padrão, segue o compotamento padrão da página.
  - *relative* posiciona o elemento de forma relativa a si mesmo no local inserido.
  - *absolute* toma como referência o elemento mais próximo com uma das caracteristicas, *relative, absolute, fixed*, se não existir, usa o como referência o *body*.
  - *fixed* o elemento irá se posicionar fixo no local inserido mesmo com scroll de página.
  - *sticky* o elemento ficará fixo quando ocorrer um scoll.
- `display: inline | block | inline-block | none | flex | grid;`  determina como o elemento será exibido em relação a página ou outros elementos.
  - *inline* torna o elemento exibido de forma que ocupe apenas a largura e altura definida, sem quebras de linha.
  - *block* o elemento sempre toma a largura inteira disponível e faz a quebra de linha.
  - *inline-block* o elemento é exibido como o *inline* porém podemos controlar e alterar largura e altura do elemento.
  - *none* o elemento não é exibido, é removido completamente da página.
  - *flex* o elemento se torna um container *flex*, habilitando o uso de **flexbox**, os elementos filhos também se tornam containers *flex*.
  - *grid* o elemento se torna um container *grid*, habilitando o uso de **grid layout**.
- `float: left | right | none | inherit;` especifica como o elemento deve se posicionar.  


## Seletores
- *Seletores* são usados para selecionar o *elemento **html** que queremos aplicar o *estilo*.
  - O *asterisco* é usado como *seletor universal*, é um seletor especial que aplica o *estilo* para todos os elementos da página html.
    <details>
      <summary>Ex:</summary>

      ```css
      * {
        margin: 0;
        padding: 0;
      }
      ```
    </details>
  - *seletor de elemento* é usado quando queremos aplicar estilização em um elemento especifico.
    <details>
      <summary>Ex:</summary>

      ```css
      p {
        color: green;
      }
      ```
    </details>
  - *seletor de classe* usado para aplicar estilização em *atributo* do tipo *class*.
    <details>
      <summary>Ex:</summary>

      ```css
      .my-class {
        color: green;
        font-size: 25px;
      }
      ```
    </details>
  - *seletor por id* usado para aplicar estilização em *atributo* do tipo *id*.
    <details>
      <summary>Ex:</summary>

      ```css
      #my-id {
        color: blue;
        font-size: 25px;
      }
      ```
    </details>
  - *seletor por atributo* é usado para especificar o estilo em todo *elemento* que conter o *atributo* desejado.
    <details>
      <summary>Ex:</summary>

      ```css
      /* all links with target defined will aplly this style */
      a[target] {
        background-color: grey;
      }
      /* Style all anchor tag that links to tutorialspoint */
      a[href="https://www.google.com"] {
        background-color: peachpuff;
      }
      ```
    </details>
  - *seletor de grupo* é usado para especificar o mesmo estilo para os elementos indicados.
    <details>
      <summary>Ex:</summary>

      ```css
      /* apply same style for h1 and h2 */
      h1, h2 {
        background-color: grey;
      }
      ```
    </details>
  - *seletor de pseudo classes* é usado para aplicar estilo em um estado especifico de um elemento.
    <details>
      <summary>Ex:</summary>

      ```css
      /* Change background color on hover */
      a:hover {
        background-color: peachpuff; 
      }
      /* Change background color on clicking button */
      button:active {
        background-color: yellow;
      }
      /* Change border color on focusing input */
      input:focus {
        border-color: blue;
      }
      ```
    </details>
  - *seletor de pseudo elemento* é usado para aplicar estilo em parte de um elemento e não ele inteiro.
    <details>
      <summary>Ex:</summary>

      ```css
      /* Define contents before paragraph */
      a::before {
        content: " ";
      }

      /* Style first letter of paragraph */
      p::first-letter {
        font-size: 2em;
      }
      ```
    </details>
  - *seletor de descendente* é usado para aplicar estilo todos as tags que são descendentes de uma tag.
    <details>
      <summary>Ex:</summary>

      ```css
      /* aplly style to all p that is inside div, no matter how deeply nested they are*/
      div p {
        color: blue;
      }
      ```
      ```html
      <h1>
        Heading text
        <div>Some content</div>
        <p>This is paragraph 1</p>
        <p>This is paragraph 2</p>
        <div>Some content</div>
        <p>This is paragraph 3</p>
      </h1>
      <!-- all p elements are descendants of h1, it would apply the color -->

      <h1>Heading text</h1>
      <p>This is paragraph 1</p>
      <p>This is paragraph 2</p>
      <p>This is paragraph 3</p>
      <!-- in this case, none would -->
      ```
    </details>
  - *seletor de filhos* é usado para aplicar estilo todos as tags filhos diretos da tag pai.
    <details>
      <summary>Ex:</summary>

      ```css
      /* apply style to remove bullet points from all li element that are direct children of a ul, are directly inside of ul. */
      h1 > p {
        color: red;
      }
      ```
      ```html
      <h1>
        Heading text
        <div>Some content</div>
        <p>This is paragraph 1</p>
        <p>This is paragraph 2</p>
        <div>Some content</div>
        <p>This is paragraph 3</p>
      </h1>
      <!-- all p elements are children of h1, it would apply the color -->

      <h1>
        Heading text
        <div>
          <p>This is paragraph 1 inside a div (won't be selected)</p>
        </div>
        <p>This is paragraph 2 (will be selected)</p>
      </h1>
      <!-- in this case, none would work because they are inside another tag-->
      ```
    </details>
  - *seletor irmão adjacente* é usado para aplicar estilo para a primeira tag na sequência da tag especificada que esteja no mesmo nível.
    <details>
      <summary>Ex:</summary>

      ```css
      /* apply color blue only to p that is next to h1 tag, if a differente tag is between h1 and p, this style will not work*/
      h1 + p {
        color : blue
      }
      ```
      ```html
      <h1>
        Heading text
        <div>Some content</div>
        <p>This is paragraph 1</p>
        <p>This is paragraph 2</p>
        <div>Some content</div>
        <p>This is paragraph 3</p>
      </h1>
      <!-- none would work -->

      <h1>Heading text</h1>
      <p>This is paragraph 1 (selected)</p>
      <p>This is paragraph 2 (not selected)</p>
      <!-- only paragraph 1 is the adjacent sibling of h1 -->
      ```
    </details>
  - *seletor irmão geral* é usado para aplicar estilo para todas as tags na sequência da tag especificada que esteja no mesmo nível.
    <details>
      <summary>Ex:</summary>

      ```css
      /* apply color blue only to p that is after to h1 tag, if more that one, all will work*/
      h1 ~ p {
        color : blue
      }
      ```
      ```html
      <h1>
        Heading text
        <div>Some content</div>
        <p>This is paragraph 1</p>
        <p>This is paragraph 2</p>
        <div>Some content</div>
        <p>This is paragraph 3</p>
      </h1>
      <!-- none would work -->

      <h1>Heading text</h1>
      <div>Some content</div>
      <p>This is paragraph 1</p>
      <p>This is paragraph 2</p>
      <!-- both Paragraph 1 and Paragraph 2 are siblings of <h1> and would be selected -->
      ```
    </details>
  - *seletor de grupo* é usado para aplicar estilo para todas as tags do grupo informado.
    <details>
      <summary>Ex:</summary>

      ```css
      /* apply color blue all elements informed*/
      h1, p {
        color : blue
      }
      ```
    </details>

## Pseudo Classes
- São usadas para selecionar e aplicar estilo em elementos de acordo com o seu estado ou posição dentro da página, sem a necessidade de usar *javascript*.
- Um exemplo do uso, seria para alterar a cor de um elemento quando passar o mouse em cima dele, ou clicá-lo.
- Usados com seletores, usando **:** após o elmemento. `a:hover{}`.
- Podemos separar em alguns tipos e categorias de uso: *Estruturante*, *interativo*, *para formulários*, *links* e *dinâmico*.
  - Alguns exemplos de *estruturantes*:
    - `:root` Tem como alvo o elemento raiz do documento.
    - `:nth-child(n)` Procura o filho nth, onde n pode ser número, palavra chave ou fórmula.
    - `:first-child` Busca o primeiro filho do elemnto.
    - `:last-child` Busca o último filho do elemento.
    - `:first-of-type` Busca o primeiro elemento do tipo especificado.
    - `:last-of-type`Busca o último elemento do tipo especificado.
  - Alguns exemplos de *interativo*:
    - `:hover` Aplica o estilo no elemento indicado ao passar o mouse por cima dele.
    - `:active` Aplica o estilo no elemento ativado, por exemplo ao ser clicado.
  - Alguns exemplos de *para formulário*:
    - `:checked` Aplica estilo no elemento checado, como em *checkbox* ou *radio button*.
    - `:valid` Alvo são elementos que tem seu valor válido dentro do formulário.
    - `:invalid` Alvo são elementos que tem seu valor inválido dentro do formulário.
  - Alguns exemplos de *link*:
    - `:link` Usado em links que ainda não foram visitados. 
    - `:visited` Usado em links que já foram visitados.
  - Alguns exemplos de *dinâmico*:
    - `:empty` Usado em elementos que não tem filhos.
    - `:not(selector)` Usado em elementos que não atendem o critério do seletor informado.
    - `:is(selector)` Usado em elementos que atendem qualquer critério do seletor informado.

## Pseudo Elementos
- São usados para estilizar partes especificas de um elemento.
- Usados com seletores, usando **::** após o elemento, `p::before{}`.
  - Alguns exemplos:
    - `::after` Usado para inserir conteúdo após o elemento.
    - `::before` Usado para inserir conteúdo antes do elemento.
    - `::first-letter` Usado na primeira letra.
    - `::first-line` Usado para a primeira linha.
    - `::placeholder` Usado para aplicar estilo em texto dentro de elementos do tipo input.
    - `::selection` Usado para estilizar texto selecionado dentro de um elemento.