# Anotaçẽs gerais sobre CSS

- [O que é CSS](#o-que-é-css)
- [Geral](#geral)
- [Seletores](#seletores)
- [Pseudo Classes](#pseudo-classes)
- [Pseudo Elementos](#pseudo-elementos)
- [Flexbox](#flexbox)
- [Grid](#grid)
- [Midia Query](#midia-query)
- [Animations](#animations)

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
- Em **CSS** podemos criar variáveis para serem reutilizadas.
- Declaração e uso de variáveis
  ```css
  :root {
    --my-var: red;
  }

  div {
    background-color: var(--my-var)
  ```
- `transition` é um atributo usado para alterar propriedades de forma suave em um período de duração.
  - Similares a animação, servem para criar alguns efeitos de transição de elementos.
  - `transition: transform 250ms;` irá aplicar no atributo `transform` a duração de 250ms.
    <details>
      <summary>Ex:</summary>

      ```html
      <!DOCTYPE html>
      <html lang="en">
        <head>
          <style> 
            .btn {
              width: 80px;
              height: 80px;
              border-radius: 50%;
              border: none;
              background: slateblue;
              color: white;
              font-size: 20px;
              font-weight: 500;
              line-height: 1;

              /*make the tranform smoother applying a transition within 250m*/
              /*we can apply transition to more than one attribute using comma and repeat the attribute and time for the transition*/
              /*
                linear is a timing function for the transition
                we can use linear, ease-in, ease-out, ease-in-out and ease, where ease is the default value.
              */
              transition: transform 250ms;
            }
        
            .btn:hover {
              transform: translateY(10px);
            }
          </style>
        </head>
        <body>
            <button class="btn">Hello</button>
        </body>
      </html>
      ```
    </details>

- `transform` serve para aplicar mudanças no elemento como: rotacionar, movimentar, inclinar, etc, através do uso de funções.
  - `translate`, `translateY` e `translateX` são funções que permitem movimentar os elementos.
    - `translateY` movimenta o elemento no eixo Y, para cima e para baixo.
    - `translateX` movimenta o elemento no eixo X, para direita e para esquerda.
    - `translate` é a forma curta para `translateX` e `translateY`, ex: `translate(1px, 10px)` *1px* representa o eixo X e *10px* representa o eixo Y.
  - `scale` é uma função que permite aumentar ou diminuir um elemento de tamanho.
    - `scale` usa valores de o até 2. Podendo passar valores para o eixo X e Y.
      - `scale(2)` dobra o tamanho, `scale(0.5, 2)` reduz metade no eixo X e dobra no eixo Y.
  - `rotate` é a função que rotaciona o elemento.
    - Podemos rotacionar em graus ou em voltas, 1 volta é 360 graus. `rotate(360deg)` ou `rotate(1turn)`.
  - `skew` é uma função usada para torcer/inclinar o elemento. Podendo ser aplicado no eixo X, eixo Y ou ambos, similar ao `translate`.
  - Podemos combinar essas funções, basta adicionar uma após a outra.

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

## Flexbox
- É um modelo de layout que fornece uma forma eficiente e flexivel de organizar e distribuir o espaço entre itens dentro do container.
- *flexbox container* define como os elementos dentro do container irão se comportar, é definido ao usar o atributo `display: flex`.
- *flexbox itens*  são filhos do item definido como container.
- *eixo principal* é a maneira como os elementos são colocados no container, por padrão o eixo principal é na horizontal.
- *eixo transversal* é o eixo perpendicular ao eixo principal, por padrão na vertical.
- Atributos usados no container:
  - `flex-direction: row | row-reverse | column | column-rever;` irá alterar o comportamento dos eixos e a distribuição dos itens dentro do container.
    - *row* é o valor padrão.
    - Se alterado para qualquer valor de *column*, o eixo principal passa a ser na vertical e o eixo transversal na horizontal.
  - `flex-wrap: nowrap | wrap | wrap-reverse;` altera como os itens se comportam em questão de quebrar para próxima linha/coluna ou tentar encaixar todos na mesma linha/coluna.
  - `justify-content: flex-start | flex-end | center | space-between | space-around | space-evenly;` altera como os itens se comportam no eixo principal. Ajuda a distribuir espaço restante da linha.
  - `align-items: flex-start | flex-end | center | stretch | baseline;` Semelhante ao `justify-content` mas para o eixo transvesal.
  - `gap: 5px;` serve para adicionar distância entre os itens dentro do container.
- Atributos usados nos itens:
  - `flex-grow: 2;` Aceita um valor número, padrão é 1, serve para definir como o item dentro do container irá crescer se necessário. Cada item dentro do container pode ter seu valor, o resultado final será distribuído de acordo. Caso existam 4 itens, três deles com `flex-grow` 1 e um deles como 2, este com maior valor terá o dobro caso tenha espaço para crescer.
  - `align-self: flex-start | flex-end | center | stretch | baseline;` Tem os mesmos valores de `align-items`, fazem a mesma coisa mas para um item especifico do container.
  - `flex-basis: 200px;` Altera o tamanho do item do container, dependendo de como está o eixo principal, afetrá `width` caso seja *row* ou `heigth` caso seja *column*.
  - `flex-shrink: 2;` É o inverso do `flex-grow`, funciona da mesma forma, porém para encolher o item.

## Grid
- É um modelo de layout mais robusto que *flexbox* e também mais complexo.
- Em um layout de *grid*, temos dois elementos: *Grid Container* e *Grid Item*
  - *Grid Container* define como é apresentado os elementos filhos dentro do container. Para usar e configurar o container, usa `display: grid;`.
  - *Grid Items* são os filhos diretos dentro do container grid, os itens podem ser posicionados verticalmente e horizontalmente.
- Por padrão, *grid* usa uma coluna única e criará as linhas conforme necessário, com base na quantidade de *grid items*.
- Para especificar e configurar colunas, usar `grid-template-columns: 50% 50%;`, no exemplo, serão duas colunas com metade do espaço disponível no container. Em *grid* ganhamos o uso de uma nova medida **fr(fraction)**, funciona de forma similar ao *flex-grow*.
  - Se usarmos `grid-template-columns: 1fr 3fe;` iremos criar uma *grid* com 2 colunas, mesmo tendo mais de 2 *grid items*, será criado uma nova linha.
- Para especificar e configurar linhas, usar `grid-template-rows: 1fr 3fr;`, no exemplo, serão duas linhas, a primeira com 1/4 do tamanho disponível e a segunda 3/4.
- Podemos especificar o número de linhas e colunas de outra forma, `grid-template-columns: repeat(3, 1fr);`, irá criar 3 colunas com o tamanho de *1fr* cada.
  <details>
    <summary>Ex:</summary>

    ```html
    <!DOCTYPE html>
    <html lang="en">
      <head>
        <style>
          .grid-container {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            grid-template-rows: repeat(4, 1fr);
          }
          /*
            in this example, we have 3 grid items, with this css we would have 3 divs in a row.
            if we add more grid items, it would follow the pattern, 3 items each row
            [1][2][3]
          */
        </style>
      </head>

      <body>
        <div class="grid-container">
          <div class="grid-item">1</div>
          <div class="grid-item">2</div>
          <div class="grid-item">3</div>
        </div>
      </body>
    </html>
    ```
  </details>
- Por padrão o algoritimo do *css grid* irá posicionar o primeiro elemento filho na primeira célula vazia. Para alterarmos esse comportamento, usamos no *grid item*, `grid-row` ou `grid-column`. Esses atributos são a forma curta de `grid-row-start` e `grid-row-end`, `grid-column-start` e `grid-column-end`, que indicam onde o *grid item* deve iniciar e terminar. Usando `grid-row` ou `grid-column`, determinar o começo e fim da posição do *grid item*.
  <details>
    <summary>Ex:</summary>

    ```html
    <!DOCTYPE html>
    <html lang="en">
      <head>
        <style>
          .grid-container {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            grid-template-rows: repeat(3, 1fr);
          }

          .grid-item {
            grid-row: 1;
            grid-column: 1 / 4;/* 1 to 4 mean the lines, 
            | | | |
            1 2 3 4
            we count the lines and not the blocks. A 4 column grid has 5 column lines. Same goes for rows.
            Negative values works, it starts counting right to left or bottom to top.
            
            grid-row: 1 is the same as grid-row-start: 1
            grid-column: 1 / 4 is the same as grid-column-start: 1 and grid-column-end: 4
            */
          }
          /*
            in this example, we have 1 grid item, this item would match the position bellow
            [1][1][1]
            [ ][ ][ ]
            [ ][ ][ ]
          */
        </style>
      </head>

      <body>
        <div class="grid-container">
          <div class="grid-item">1</div>
        </div>
      </body>
    </html>
    ```
  </details>
- Existe uma forma diferente de organizar itens dentro da *grid*, usando *grid areas*.
  <details>
    <summary>Ex:</summary>

    ```html
    <!DOCTYPE html>
    <html lang="en">
      <head>
        <style>
          .grid-container {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            grid-template-rows: repeat(3, 1fr);
          }

          .grid-item {
            grid-row: 1;
            grid-column: 1 / 4;        
          }
        </style>
      </head>

      <body>
        <div class="grid-container">
          <div class="grid-item">1</div>
        </div>
      </body>
    </html>
    ```
  </details>
  

## Midia Query
- São regras que permitem estiliação de página para certos tamanhos de tela. Ajudam a manter a *responsividade* para diversos dispositivos com telas em tamanhos diferentes.
- Se a *media query* configurada for compatível com o tamanho de tela no dispositivo, a regra será aplicada.
  <details>
    <summary>Sintaxe:</summary>

    ```html
    <!DOCTYPE html>
    <html lang="en">
      <head>
        <style>
          /*
          @media [media-type] ([media-feature]) {
             CSS Styles 
          }
          */
        </style>
      </head>
      <body>
        <h1>MEDIA QUERY</h1>
      </body>
    </html>
    ```
  </details>
- *Media Types* são usados para aplicar **CSS** em diferentes tipos de dispositivos. Os mais comuns são: *all*, *print* e *screen*.
  - *all* é o valor padrão, usando este valor, todos os dispositivos seguirão o estilo aplicado.
  - *print* serve para quando queremos imprimir a página.
  - *screen* só serve para telas, como computadores, tablets e celulares.
- *Media Fetures* aplicam o estilo com base em características específicas, todas as *media features* devem ter *parenteses* ao redor.
- *Operadores lógicos* são usados para definir as regras de estilização que queremos aplicar. Podendo ser usados em combinação da forma que for necessária para atingir o resultado esperado. São eles:
  - *and* combina múltiplos *media features*, onde cada resultado precisa ser *true*.
  - *or* similar ao *and* mas apenas uma das condições precisa ser *true*.
  - *not* usado para reverter a lógica da condição.
  - *only* aplica o estilo, apenas se toda a condição for *true*.
  - *comma(,)* combina uma ou mais condições em uma.
  <details>
    <summary>Ex:</summary>

    ```html
    <!DOCTYPE html>
    <html lang="en">
      <head>
        <style>
          /* in this example, the layout will change when less than 992px from 4 columns to 2, when it's less than 500px will change from 2 to 1*/
          .column-box {
            float: left;
            width: 25%;
            padding: 3px;
            box-sizing: border-box;
            background-color: pink;
            border: 2px solid blue;
        }
          @media screen and (max-width: 992px) {
              .column-box {
                width: 50%;
              }
          }
          @media screen and (max-width: 500px) {
              .column-box {
                width: 100%;
              }
          }
        </style>
      </head>
      <body>
        <h2>Resize the browser window to see the effect.</h2>
        <div class="column-box">Box 1</div>
        <div class="column-box">Box 2</div>
        <div class="column-box">Box 3</div>
        <div class="column-box">Box 4</div>
      </body>
    </html>
    ```
  </details>

## Animations
- **CSS** permite animação dos *elementos* *html* sem que seja necessário o uso de *javascript*.
- Uma animação é a alteração gradualmente de um estilo para outro.
- Para usar animações, precisamos fazer o uso de **keyframes**. **Keyframes** são usados para definir animações, especificando a sequência de quadros ou passos da animação.
  - Sintaxe: `@keyframes animation-name {keyframes-selector {css-styles;}}`.
    - *animation-name* é obrigatório, serve para identificar o nome do **keyframe** que irá ocorrer a animação.
    - *keyframe-selector* é o tipo de seletor que usaremos para animação, ex: `from(0%)`, `to(100%)`.
  <details>
    <summary>Ex:</summary>

    ```html
    <!DOCTYPE html>
    <html lang="en">
      <head>
        <style>
          .box {
            width: 100px;
            height: 100px;
            background-color: pink;
            display: grid;
            place-content: center;
            color: white;
            text-align: center;

            animation: slide-in 1000ms;
            /*if the iteration count needed to be inifite, just change 3 to infinite*/
            animation-iteration-count: 3;
          }

          /*
            creates an animation that will slide from left to right
            slide-in is the name of the animation, must be unique
          */
          @keyframe slide-in {
            from {
              transform: translateX(-100%);
              opacity: 0.25;
            }
            to {
              transform: translateX(0%);
              opacity: 1;
            }
          }
          
        </style>
      </head>
      <body>
        <div class="box">Hello</div>
      </body>
    </html>
    ```
  </details>
- Caso queira adicionar delay na animação, usar o atributo `animation-delay`.
- Podemos modificar o fluxo que a animação é executada com `animation-direction`. Podemos mudar para executar de trás pra frente, normal, alternado e alternado reverso.
  - `animation-direction: normal;` é o padrão, a aplicação roda normalmente.
  - `animation-direction: reverse;` muda para o fluxo reverso, de trás pra frente.
  - `animation-direction: alternate;` usado para animação que começa e retorna ao início, vai no fluxo normal e retorna em reverso.
  - `animation-direction: alternate-reverse;` similar ao *alternate* mas no sentido reverso.
- Podemos especificar a curva de velocidade usada na animação. Quando movemos um elemento da esquerda para direita, o elemento se move de forma linear, podemos alterar esse comportamento linear para outros.
  - `animation-timing-function: linear` é o comportamento descrito acima.
  - `animation-timing-function: ease` é o valor padrão quando não alterado.
  - `animation-timing-function: ease-in` a animação começa lento e finaliza rápido.
  - `animation-timing-function: ease-out` a animação começa rápido e finaliza lento.
  - `animation-timing-function: ease-in-out` é a combinação de *easy-in* com *easy-out*.