# Anotaçẽs gerais sobre HTML

- [O que é HTML](#o-que-é-html)
- [Geral](#geral)
- [Tags](#tags)
- [Atributos](#atributos)

## O que é HTML
- HTML é um marcador padrão para páginas web.
- HTML significa HyperText Markup Language
- Usado para criar conteúdos e estruturar páginas web.
- Criado em 1991 por Berners-Lee

## Geral
- HTML é formados por elementos e estes elementos possuem uma hierarquia, podemos criar elementos dentro de outros elementos.
- Existem algumas regras que devem ser seguidas para estruturar uma página HTML.
- **tags** são paralavras chaves para representar com o navegador web irá apresentar e formatar a página **html**.
- *elementos html* são blocos para contruir a página web. Consistem em **tag** de abertura e **tag** de fechamento e o conteúdo dentro.
- *atributos html* são usados para customizar os *elementos html* e adicionar comportamento para eles, usados dentro da abertura da **tag** para modificar o *elemento*.
- Exemplo básico de um documento:
```html
<!-- HTML Version Declaration -->
<!DOCTYPE html>
<!-- HTML Root Element -->
<html>

<!-- HTML Head Section -->
<head>
    <!-- HTML Document Title -->
    <title>This is Title</title>
</head>

<!-- HTML Body Section -->
<body>
    <!-- HTML Header Element -->
    <h1>This is Header</h1>
    <!-- HTML Paragraphs Element -->
    <p>This is a Paragraph</div>
</body>
</html>
```
- `<!DOCTYPE html>` é a **tag** que define que o documento ẽ **html** e qual versão a ser usada.
- `<html>` essa **tag** engloba o documento **html** completo e é composta principalmente pelo cabeçalho do documento, que é representado pelas tags `<head>...</head>`, e o corpo do documento, que é representado pelas tags `<body>...</body>`.
- `<head>` representa o cabeçalho do documento **html**. 
- `<title>` usado dentro da **tag** `<head>` para adicionar o título do documento.
- `<body>` represeta o conteúdo do documento **html**.
- `<h1>` até `<h6>` serve para especificar cabeçalhos para o conteúdo.
- `<p>` representa paragráfo dentro do conteúdo **html**.
- Para adicionar comentários em **html**. usar `<!-- my comment here -->`.
- Os *elementos* **html** podem ser divididos em duas formas: elementos de bloco e elementos em linha.
  - *elementos em bloco* são aqueles que a **tag** abre e fecha, `<tag> ... </tag>` e que ao serem usados, irão fazer a quebra de linha automaticamente.
  - *elementos em linha* são aqueles que a **tag** abre e fecha, `<tag />` e não fazem a quebra de linha quando usados.

## Tags
- `<br/>` usado para quebra de linha, ao adicionar esta **tag**, será adicionado uma nova linha, caso tenha algo na sequência, irá para a próxima linha.
- `<center>` usado para adicionar conteúdo no centro.
- `<hr/>` cria uma linha na horizontal no local adicionado.
- `<pre>` usado para preservar o formato do texto, manterá a mesma formatação do texto adicionado.
- `<b>` usado para adicionar negrito.
- `<i>` usado para adicionar itálico
- `<del>` usado para adicionar texto com formato de deletado.
- `<img>` usado para adioncar imagem, é uma **tag** vazia, não possui uma **tag** para abertura e outra para fechamento, `<img src="path/image" />`
  - **alt** é um *atributo* para adicionar texto alternativo caso a imagem não seja carregada.
- `<meta>` usada para especificar metadados, colocar dentro da **tag** *head*.
  - `<meta name="keywords" content="HTML, Meta Tags, Metadata" />` adiciona palavras chaves para o documento, melhora a visualização e busca da página em sistemas de busca como o google.
  - `<meta http-equiv="refresh" content="5" />` especifica um tempo de duração ao qual a página web ficará sendo recerregado automaticamente.
  - `<meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />` serve para alterar o formato de enconding do conteúdo da página.
- `<table>` permite criar tabelas de dados.
  - `<table>` é usado para criar a tabela.
  - `<tr>` usado para representar linhas dentro da tabela.
  - `<th>` usado para representar colunas de cabeçalho.
  - `<td>` usado para representar dados dentro da tabela.
  - **border** cria uma borda ao redor das linhas e colunas da tabela.
- `<ul>` usado para criar lista que não possuem ordem.
  - `<ul>` cria a lista.
  - `<li>` identifica o item da lista.
- `<ol>` usado para criar listas ordenadas.
  - `<ol>` cria a lista.
  - `<li>` identifica o item da lista.
- `<a>` usado para criar um texto do tipo link.
  - **href** indica qual o destino do link. Podendo ser usado *ids* como referência e direcionar para o *id* informado.
  - **target** especifica onde será aberto o link.
    - *_blank* abre em uma nova janela ou aba.
  - **download** usado quando queremos criar um link com download da referência de um arquivo.
- `<form>` cria um formulário para coleta de dados. Apenas a **tag** sozinha não é o suficiente, precisa conter outras **tags** em conjunto para informar os dados.
  - Todo formulário possui uma **action**, sem valor irá enviar os dados para a mesma **URL** que o formulário se encontra.
  - **method** define o tipo de envio dos dados do formulário. **GET** e **POST** são os mais comuns. Caso não informado, **GET** será o valor padrão.
  - Ao menos um tipo de entrada de dados precisa ser coletado para o formulário funcionar.
  - `<button>` ou `<input>` para envio dos dados é obrigatório para fazer o envio dos dados.
  - Ex:
  ```html
    <form action="/submit" method="POST">
        <label for="name">Name:</label>
        <input type="text" id="name" name="name"><br>

        <label for="email">Email:</label>
        <input type="email" id="email" name="email"><br>

        <input type="submit" value="Submit">
    </form>
  ```
  - `<input>` é uma das maneiras de coletar dados no formulário.
  - `<label>` adiciona uma descrição para o *input*, usando o **atributo** *for* para fazer o link com o *id* do *input*.
  - No exemplo foi usado um *input* para envio dos dados, poderia ser usado um botão: `<button type="submit">Submit</button>`.

- `<input>` esta **tag** pode conter vários formatos de coleta de dados, algun deles são:
  - `<input type = "text">` para coletar dados de texto.
  - `<input type = "number">` para coletar dados numérios.
  - `<input type = "checkbox">` é exibido como uma caixa quadrada, que pode ser marcada ou desmarcada de acordo com a necessidade do dado coletado.
  - `<input type = "radio">` similar ao *checkbox* porém apenas um dos itens será escolhido.
  - `<input type = "date">` para selecionar uma data.
  - `<input type = "month">`  para selecionar um mês.
  - `<input type = "range">`  para selecionar um range de valores.
  - `<input type = "email">`  para coletar dados do tipo email.
  - `<input type = "url">`  para coletar dados do tipo link.
  - `<input type = "password">`  para coletar dados de senha.
  - `<select>` é usado para criar uma lista de escolhas.
  - `<textarea>` usado para coletar dados de texto grande, maiores que apenas uma frase.
- `<video>` usado para adicionar vídeo na página.
  - Ex:
  ```html
  <video width="450" height="250" controls>
   <source src="url/of/video" type="video/webm">
  </video>
  ```
  - **controls** habilita uma interface com algumas funcionalidade como, pause, avançar e voltar o vídeo.
  - `<source>` é onde o vídeo pode ser encontrado e o formato do vídeo. Para habilitar outros formatos, adicionar mais **tags** *source* com outros formatos.
- `<audio>` funciona similar ao vídeo, para adicionar audio na página.
  - Ex:
  ```html
  <audio controls>
   <source src="url/of/audio" type="audio/mp3">
  </audio>
  ```
- `<div>` é um elemento de bloco usado para servir de container para outras **tags**, fazendo um agrupamento e podendo melhorar a aparência da página.
  - Para melhorar o layout da página, podemos usar algumas **tags** que fazem o mesmo papel das *divs*, porém com um propósito de estruturação de tela.
  - `<header>` usado para definir uma seção do tipo cabeçalho.
  - `<nav>` representa uma seção que contém links para outras páginas ou para sí mesmo.
  - `<main>` define o conteúdo principal da página.
  - `<section>` quebra em seções o conteúdo principal da página.
  - `<footer>` representa o rodapé da página. Sempre estará no final da página, geralmente usado para informações de copyright.
  - `<aside>` seção que contém conteúdo ligado direto ou indiretamente ao conteúdo principal, uma seção na lateral do *main*

## Atributos
- Atributos podem ser genéricos ou específicos, somente usados por elementos especificos.
- **id** usado para identificar de forma única um elemento. `<p id="one"></p>`.
- **title** adiciona um título para o elemento, será exibido ao colocar o mouse em cima do elemento com o atributo.
- **class** semelhante ao *id*, porém pode haver repetição, muito usado para estilização com **CSS**.
- **style** usado para adicionar **CSS** diretamente no elemento.
- **dir** usado para indicar qual a direção o navegador exibirá o texto. Possui dois valores apenas, *ltr* (left to right) e *rtl* (right to left). `<html dir"rtl">`
- **width** serve para especificar a largura de um *elemento*
- **heigth** serve para especificar a altura de um *elemento*