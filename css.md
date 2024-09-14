# Anotaçẽs gerais sobre CSS

- [O que é CSS](#o-que-é-css)
- [Geral](#geral)

## O que é css
- **CSS** é uma linguagem para estilização da página web.
- **CSS** significa *Cascading Syle Sheets*.
- Com o **css** conseguimos alterar o comportamento do **html**.
- Podemos aplicar **css** de três formar no **html**:
  - *em linha* é aplicado diretamente no *elemento* **html** e assim se torna o prioritário em questão de qual *estilo* será processado.
  - *interno* é definido na *tag* *head* do **html**, dentro do *head* insere-se um *elemento* `<style>`.
  - *externo* é definido separadamente em um outro arquivo, para importar o **css** *externo*, adicionar uma *tag* `<link>` com a referência do arquivo.
  - Ex:
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
- *Seletores* são usados para selecionar o *elemento **html** que queremos aplicar o *estilo*.
  - O *asterisco* é usado como *seletor universal*, é um seletor especial que aplica o *estilo* para todos os elementos da página html.
    - Ex:
    ```css
      * {
        margin: 0;
        padding: 0;
      }
    ```
  - *seletor de elemento* é usado quando queremos aplicar estilização em um elemento especifico.
    - Ex:
    ```css
      p {
        color: green;
      }
    ```
  - *seletor de classe* usado para aplicar estilização em *atributo* do tipo *class*.
    - Ex:
    ```css
      .my-class {
        color: green;
        font-size: 25px;
      }
    ```
  - *seletor por id* usado para aplicar estilização em *atributo* do tipo *id*.
    - Ex:
    ```css
      #my-id {
        color: blue;
        font-size: 25px;
      }
    ```
  - *seletor por atributo* é usado para especificar o estilo em todo *elemento* que conter o *atributo* desejado.
    - Ex:
    ```css
      /* all links with target defined will aplly this style */
      a[target] {
        background-color: gray;
      }
    ```