# Anotações gerais sobre Linux

## Geral

- O diretório que contém as informações de comando do linux se encontra em: **/bin**.
- Para verificar qual versão do linux instalada, usar:
    - `cat /etc/os-release`
    - `hostnamectl`
- O diretório *root* do linux se encontra em **/**.
- Dentro de *root* existe uma hierarquia do sistema de arquivos do linux.
    - **/bin/** comandos essenciais do usuário em binário.
    - **/boot/** arquivos essenciais para ínicio do sistema.
    - **/dev/** arquivos de dispositivos conectados.
    - **/etc/** contém configurações específicas dos sistema.
    - **/home/** diretórios dos usuários cadastrados.
    - **/lib/** bibliotecas essenciais compartilhadas usadas pelos binários encontrados em **/bin** e **/sbin**.
    - **/media/** local onde se encontra media de dispositivos removíveis.
    - **/mnt/** sistemas temporários montados.
    - **/opt/** aplicações opcionais.
    - **/sbin/** binários do sistema.
    - **/srv/** dados de serviços dos sistema.
    - **/tmp/** arquivos temporários.
    - **/usr/** aplicaçẽos dos usuários.
    - **/var/** arquivos variáveis em tamanho e conteúdo conforme o sistema está rodando, exemplos são logs e arquivos
      temporários.
    - **/root/** diretório para arquivos do usuário root.
    - **/proc/** informações de processos.
- Para criar arquivos de maneira rápida e escrever sem precisar abrir em um editor, podemos usar:
    - `echo linha um > file`
    - `echo linha dois >> file`
    - `echo linha tres >> file`
    - Fazendo isso teremos um arquivo chamada **file** com as 3 linhas que informados.
    - Usando um único *>* irá sobreescrever o conteúdo do arquivo.
    - Usando *>>* irá adicionar no final, concatenar no conteúdo do arquivo.
    - Uma outra forma de seria usando `cat` para criar um arquivo.
        - `cat > another.txt` irá habilitar entrada de texto no terminal, podendo digitar e ir para próxima linha com
          *enter*. Para finalizar e salvar no arquivo, apertar *Ctrl + d*.
- Para adicionar novas variáveis no linux, pode ser usados algumas formas diferentes:
    - Adicionar permanentemente, podendo ser adicionado em um dos arquivos: **~/.bashrc** ou **~/bash_profile**
        - Abrir um dos arquivos mencionados e adicionar a variável no arquivo, `export VARIABLE=value`.
        - No terminal digitar o comando `source ~/.bashrc` ou `source ~/.bash_profile` para fazer o load do arquivo no
          sistema.
        - No caso do **bashrc** não é necessário fazer o load pois este load sempre é feito ao abrir um novo terminal.

## Comandos

- `man` (manual) meio de mostrar ajuda para comandos.
    - `man ls` manual de uso do `ls`.
- `-h` ou `--help` mostra informações de ajuda para comandos.
    - `ls -h` ajuda pra `ls`.
- `sudo` (super user do) habilita o uso de comandos como root.
- `whoami` mostra quem é o usuário logado.
- `clear`  limpa o terminal.
- `ls` (list) lista o conteúdo do diretório.
    - `ls -l` para usar um formato longo de lista.
    - `ls -a` para mostrar arquivos ocultos, que começam com . (ponto) antes do nome.
- `cd` (change directory) muda de diretório.
    - `cd Documents` vai pra Documents.
    - `cd ..` volta um diretório.
    - `cd -` vai para o diretório que estava por último.
- `pwd` (print working directory) mostra o diretório.
- `mkdir` (make directory) cria um diretório.
- `rm` (remove) serve para remover coisas (arquivos, diretórios).
    - `rm file` remove arquivo com nome file.
    - `rm -r folder` remove recursivamente os subdiretórios.
    - `rm -f folder` remove forçando a remoção com arquivos dentro do diretório.
- `cp` (copy) copiar um arquivo.
    - `cp file.txt ~/Downloads/` copia o arquivo para diretório especificado.
- `mv` (move or rename) move ou renomeia arquivos.
    - `mv file.txt file2.txt` renomeia o arquivo.
    - `mv file.txt ~/Downloads/` move o arquivo para diretório especificado.
- `touch` cria um arquivo.
    - `touch arquivo.txt`
- `cat` serve para mostrar o conteúdo de um arquivo.
- `find` serve buscar arquivos.
    - A estrutura de `find` é: `find <DIR_TO_START> <OPTIONS> <SEARCH_TERM>`.
        - *DIR_TO_START* é o diretório de origem onde a busca irá começar.
        - *OPTIONS* é dedicado para o arquivo a ser buscado, como nome, tipo, data de criação do arquivo, etc.
    - Tipo de buscas usando `find`:
        - Por nome: `find . -name <FILE>`, onde **.** é o diretório atual e **FILE** é o nome do arquivo a ser buscado.
        - Por tipo: `find ~ -type d`, onde **~** é o diretório **home** do usuário logado e *d* seria para diretórios.
            - **d** diretório.
            - **f** arquivo.
        - Por tamanho do arquivo: `find ~ -size 10M`.
            - c – bytes
            - k – kilobytes
            - M – megabytes
            - G – gigabytes
    - `find /home/ -name *.txt` encontrar qualquer arquivo com extensão txt, partindo do diretório **home**.
    - `find /home/ -name ?.txt` encontrar qualquer arquivo com extensão txt, que tenha um caracter antes do .txt,
      partindo do diretório **home**.
    - `find /home/ -name [a-z].txt` encontrar qualquer arquivo com extensão txt, que tenha um caracter dentro do
      carateres informados entre **[ ]** do .txt, partindo do diretório **home**.
    - `find` pode ser usado para encontrar arquivos e executar comandos com os arquivos encontrados.
        - `find ~ -name *.rs -exec cat {} \;` irá encontrar todos os arquivos que tenham extensão .rs e ler o conteúdo
          dos arquivos encontrados.
            - `-exec` é o que faz executar um comando.
            - Após o `-exec` foi passado o comando `cat`.
            - Os **{}** servem como uma lista e recebem/adicionam todos os arquivos encontrados nela.
            - Precisa ter o **\;** ou **';'** para finalizar a expressão.
- `head` serve para mostrar as primeiras linhas de um arquivo.
- `tail` serve para mostrar as ultimas linhas de um arquivo.
- `echo` serve para imprimir algo no terminal.
    - `echo "Oi"` imprimi Oi no terminal.
    - `echo "oi" > oi.txt` criar um arquivo com o nome informado e adiciona o texto no arquivo.
        - Se repetir o comando, o conteúdo será sobreescrito.
        - Para concatenar, usar `echo "tchau" >> oi.txt`
- `wc` (word count) serve para contas linhas, palavras e characteres de arquivos.
    - `wc file.txt` irá contar linhas, palavras e bytes.
    - `wc -l file.txt` irá contar o número de linhas.
    - `wc -c file.txt` irá contar o número de bytes.
    - `wc -w file.txt` irá contar o número de palavras.
- `sed` (stream editor) é um comando usado para modificar o conteúdo de um arquivo ou texto, geralmente adicionando o
  novo conteúdo em um novo arquivo.
    - Se usarmos `sed s/unix/linux file.txt` irá substituir a primeira palavra de cada linha que tiver *unix* por
      *linux*.
    - Se usarmos `sed s/unix/linux/2 file.txt` irá substituir a segunda palavra de cada linha que tiver *unix* por
      *linux*.
    - Se usarmos `sed s/unix/linux/g file.txt` irá substituir todas as palavras *unix* por *linux*.
    - Se usarmos `sed s/unix/linux/g file.txt > file2.txt` irá criar um outro arquivo e substituir todas as palavras
      *unix* por *linux*.
- `awk` é usado para extrair e printar conteúdos específicos de arquivos.
    - `awk '{print $0}' /etc/passwd` imprimi todo o conteúdo do arquivo, igual ao `cat /etc/passwd`
    - `awk -F: '{ print $1 }' /etc/passwd` imprimi a primeira coluna de cada linha.
        - `-F` especifica o separador que queira usar por cada coluna, no exemplo `-F:` irá separar cada coluna por **:
          **.
    - `awk -F: '{ print $1 $7 }' /etc/passwd` imprimi a primeira e sétima coluna de cada linha.
- `grep` (global regular expression print) serve para procurar por textos.
    - `cat ~/.profile | grep export` busca a palavra *export* dentro do arquivo.
    - `cat ~/.profile | grep -v export` mostra o conteúdo do arquivo que não tenha a palvra *export* dentro do arquivo.
    - `cat ~/.profile | grep -n export` busca a palavra *export* dentro do arquivo enumerando a linha que se encontra a
      palavra.
    - `cat ~/.profile | grep -i export` busca a palavra *export* dentro do arquivo de forma a ignorar palavra maiúscula
      de minúscula.
    - `cat ~/.profile | grep -c export` conta quantas vezes a palavra *export* dentro do arquivo.
    - `cat ~/ | grep -r export` busca a palavra *export* dentro do arquivo de forma recursiva que entre nas subpastas.
- `sort` é usado para fazer a organização das linhas de um texto de forma ordenada.
    - `sort file.txt` irá ordenar de forma ascendente.
    - `sort -r file.txt` irá ordenar de forma revertida.
- `strings` é usado para localizar textos legíveis em arquivos binarios, como planilhas do excel, pdf, etc.
    - `string file.xlsx` irá retornar as palavras legíveis para humanos encontradas no arquivo informado.
- `ln` server para criar links de arquivos e diretórios no sistema. Podendo ser usado para ter um mesmo arquivo em um
  local diferente de acesso.
    - Exemplo de uso nas configurações do neovim com link para o repositório do git.
    - `ln -s ~/Documents/projects/dotfiles/nvim ~/.config/nvim` irá criar um link com as configurações do git para a
      pasta de config do neovim.
    - Para remover o *symlink* usar `unlink ~/.config/nvim`
- `adduser` adiciona um novo usuário.
- `which` para encontrar onde um comando se encontra.
    - `which ls` mostra onde se encontra o comando ls.
- `ps` (process status) mostrar os processos rodando.
- `wget` é usado para fazer download usando links.
- `curl` (client url) usado para fazer diferentes tipos de chamdas (http, ftp).
    - `curl -I https://google.com` faz uma chamada GET para o site indicado e traz apenas os headers da resposta.
- `alias` serve para criar apelidos para comandos.
    - `alias la="ls -al` cria apelido para comando indicado.
    - `alias` no terminal n é permante, para tornar permanente, adicionar em **~/.bashrc**.
- `xrandr` para mostrar informações dos monitores.
- Para adicionar variáveis de ambiente, usar:
    - `export VARIABLE_NAME=VARIABLE_VALUE`, dessa forma é adicionado mas o valor não fica salvo após encerrar a sessão.
    - Para salvar na sessão do usuário:
        - Abrir o arquivo em modo de edição: `nano ~/.bash_profile`
        - Inserir a variável: `export VARIABLE_NAME=VARIABLE_VALUE`
        - Aplicar as mudanças: `source ~/.bash_profile`
- Usar `sudo passwd USER_NAME` para mudar a senha do usuário informado.
- `df` (disk free) para mostrar a quantidade de espaço livre e usado.
    - `df -H` o `-H` é pra ajudar na forma de apresentação para uma leitura mais humana.
- `tar` é um comando usado para compactar e descompactar arquivos.
    - `tar -cvf file.tar ~/file` irá criar um arquivo tar como nome *file.tar* partindo do arquivo encontrado em *~
      /file*.
    - `tar -xvf file.tar` irá descompactar um arquivo do tipo tar no diretório atual.
    - Opções disponíveis no comando `tar`:
        - *c* cria um novo arquivo .tar
        - *v* mostra uma descrição do progresso de compactação.
        - *f* nome do arquivo.
        - *z* adiciona o formato de compressão/descompressão **gzip**, usado em arquivo com extensão **.tar.gz**.
- `traceroute` é usado para inspecionar a rota que o pacote de dados da internet pega até chegar no *host*
    - `traceroute www.google.com` irá mostrar a rota de dados até o host do google.
- `bluetoothctl` é um comando para funcionalidade de bluetooth.
    - Digitar `bluetoothctl` no terminal irá habilitar o shell interativo.
    - `bluetoothctl scan on` faz 0 scan para descobrir os dispositivos disponíveis. *Ctrl + z* para parar a busca.
    - `bluetoothctl devices` para listar os dispositivos encontrados no scan.
    - `bluetoothctl pair <DEVICE_MAC>` faz o pareamento usando o mac address do dispositivo encontrado.
    - `bluetoothctl connect <DEVICE_MAC>` para conectar com o dispositivo.
    - `bluetoothctl disconnect <DEVICE_MAC>` para desconectar o dispositivo.

## WSL

- No windows 10 ou mais atual podemos rodar e instalar uma versão de linux sem precisar de uma máquina virtual.
- Instalação:
    - Rodar o comando em modo administrador, instala Ubuntu por padrão: `wls.exe install`
    - Reiniciar o windows e habilitar o wls2 como padrão: `wsl --set-default-version 2`
    - Listar distribuições linux: `wsl --list --online`
    - Instalar a versão escolhida da lista: `wsl --install -D Debian`
    - Alterar a distribuição linux padrão: `wls --set-default Debian`
    - Para atualizar a versão do linux: `wsl --update`
    - Alterar o uso da versão do wls para a distribuição do linux: `wsl --set-version Debian 2`
    - As distribuições ficam instaladas no *disco C:*
    - Para acessar os arquivos linux através do windows, usar o caminho: `\\wsl$\`
    - Para acessar arquivos do windows através do linux, usar o caminho: `/mnt/c/Users/`

## Bash

- *Shell* é uma ferramenta que nos permite executar comandos no terminal.
- *Bash* significa, born again shell.
- `#!/usr/bin/env bash` chamado de *shebang*, usado na primeira linha para identificar que o script é do tipo bash
  script.
    - Apenas o *shebang* é necessário para entender que o arquivo é do tipo *bash*, sendo assim não precisa adicioanr
      *.sh* na extensão do arquivo.
- Para executar o *script*, normalmente usamos **./** e o nome do arquivo *bash*. Se não fizermos desta forma, o sistema
  tentará localizar o *script* em um dos diretórios dentro da variável de ambiente **$PATH**.
- Caracteres especiais usados no **bash**:
    - **#** usado para criar comentários
    - **\** usado no final da linha para indicar continuação na próxima linha ou para indicar que o próximo caractere
      precisa ser interpretado literalmente, `\$` irá usar o *$* como caractere.
    - **;** usado para interpretar que o que segue a partir dele será um novo comando a ser executado:
        - `mkdir newDir ; cd newDir ; pwd`, diferente de `mkdir newDir && cd newDir ** pwd`, usando *&&* o próximo
          comando só irá executar se o atual não falhar.
    - **$** indica que o depois dele é uma variável.
    - **>** redirecionamento de saída, é o processo de enviar a saída de dados de um comando para um arquivo.
    - **>>** concatenação de saída, é o processo de concatenar a saída de dados de um comando para um arquivo.
    - **<** redirecionamento de entrada, ao contrário do de saída, o conteúdo de um arquivo é redirecionado para um
      comando.
    - **|** usado para combinar o resultado do comando atual para o próximo comando.
- Em *bash* podemos passar parâmetros ao rodar o sistema, esses parâmetros são acessados da seguinte forma:
    - **$0** para o nome do arquivo *bash*.
    - **$1**, **$2** e assim por diente para os próximos parâmetros.
    - **$@** para acessar todos os parêmtros.
    - **$#** para mostrar a quantidade de parâmetros informados.
  ```bash
      #!/usr/bin/env bash

      #runing as ./script first
      echo "Entered argument: $1"
      #echo will print: Entered argument: first
  ```
- Podemos usar comandos para serem adicionados em variáveis ou como parte de outros comandos. Para isso usamos **$()**.
    - Ex: `ls /lib/modules/$(uname -r)/`, `uname -r` irá retornal algo como *6.2.4* e será inserido como argumento no
      comando `ls`.
- `env` para listar variáveis do sistema.
- `echo $SHELL` mostra qual *shel* está configurado como padrão.
- `which bash` mostra a localização do *bash*.
- `chmod +x <FILE>` é o comando usado para mudar permissiões de arquivos e diretórios, o *x* libera permissão para
  execução do arquivo.
    - Arquivos têm 3 tipos de permissões, **r** para ler, **w** para escrever e **x** para executar.
    - Além das permissões dadas, temos quais grupos queremos afetar, **u** para usuário, **g** grupo e **o** outros.
    - Quando executamos o comando `ls -l file` o retorno pode seguir o seguinte formato `-rw-r--r-- 1 ...`. Usuário tem
      *rw*, grupo *r* e outros *r*.
    - Existe uma forma mais simples de alterar permissões de acesso para arquivos.
        - 1 para executar.
        - 2 para escrever.
        - 4 para ler.
        - `chmod 111 file` dá permissões para executar o arquivos nos 3 grupos(**u,g e o**).
        - Podendo combinar/somar cada um, `chmod 765 file`, usuário pode ler,escrever e executar, grupo pode ler e
          escrever, outros pode ler e executar.
- Para verificar se um comando foi bem sucedido, temos no bash *exit codes*.
    - São uma forma de verificar se o último comando foi executado com sucesso.
    - Se eu rodar qualquer comando, para verificar se ele teve sucesso, verificar o valor de `$?`
    - Ex: `sudo dnf install notexist` e depois `echo "$?"`. Em caso de sucesso, o retorno será 0, qualquer erro terá o
      código diferente de 0.
    - Ao usarmos **exit 1** no script, ele irá encerrar a partir dele e não rodas as linhas seguintes.
- Caso queira criar um script universal, para verificar qual o gerenciador de pacotes, buscar em */etc/*, exemplos:
  */etc/dnf*, */etc/apt/*.
- Existem algumas maneiras de manipular *string* em bash.
    - Usar `length=${#string}` para pegar o tamanho da *string*.
    - Usar `name="Test string"; echo ${name:0:4}`, irá fazer o print de *Test*.
        - `${name:0:4}`, o *0* é qual a posição da *string* iremos começar e o *4* são quantos caracteres queremos pegar
          a partir da posição que indicamos.
- Temos como rodar o script habilitando uma forma de debug. Usando `bash -x ./script` irá habilitar o modo debug.
- Para ler entrada de dados do terminal:
  ```bash
      #!/usr/bin/env bash

      echo "Enter your name:"
      read name
      echo "Your name is $name."
  ```
    - Podemos concatenar dados de variáveis usando **${ }**.
      ```bash
        #!/usr/bin/env bash
  
        echo "What are you doing?"
        read action
        echo "You are ${action}ing."
      ```
- *Subshell* são comandos realizados de forma apartada. Ex:
  ```bash
      #!/usr/bin/env bash

      number=1
      
      #commands inside parentheses run as subshell
      (
        number=2
        echo "subshell number: $number"
      )
      echo "number: $number"
      #will echo
      #subshell number: 2
      #number: 1
  ```
- **Variables**:
    - Variáveis dentro do código:
      ```bash
        #!/usr/bin/env bash
  
        #variable declaration
        name="Fulano"
  
        #using double quotes will print variable value, single quotes will print literals
        echo "Hello $name"
      ```
    - Variáveis inseridas através de comandos:
      ```bash
        #!/usr/bin/env bash
  
        #use commands as variables
        files=$(ls)
  
        echo "$files"
      ```
- **Math**:
    - Bash usa expressões matemáticas de forma diferente.
    - Para fazer cálculos em bash, usar: `$(())`, os espaços são importantes.
        - Soma: `$(( 1 + 2 ))`
        - Subtração: `$(( 2 - 1 ))`
        - Divisão: `$(( 2 / 2 ))`
        - Multiplicação: `$(( 2 * 2 ))`
        - Módulo: `$(( 5 % 2 ))`
        - Exponencial: `$(( 5 ** 2 ))`
    - Existe uma outra forma, porém deprecada usando `expr`.
        - Soma: `expr 8 + 8`
        - Subtração: `expr 8 - 8`
        - Divisão: `expr 8 / 8`
        - Multiplicação: `expr 8 * 8`
        - Módulo: `expr 5 % 2 `
        - Exponencial: `expr 5 ** 2 `
    - Para adicionar o resultado em uma variável, usar: `a=$(( 8 + 8 )) ; echo $a` ou `let x=( 8 + 8 ) ; echo $x`.
- **If statements**:
  ```bash
      #!/usr/bin/env bash
      
      mynum=200

      #numerical tests
        #eq - equal
        #ne - not equal
        #gt - greater tha
        #lt - less than
        #ge - greater than or equal
        #le - less than or equal
      #string test use ==
      #more conditions check man test
      #use brackets to delineate the test condition and space after and before each bracket
      if [[ $mynum -eq 200 ]]
      then
        echo "Number is 200"
      elif [[ $mynum -lt 200 ]] ; then
        echo "Number is less than 200"
      elif [[ $mynum -gt 200 ]] ; then
        echo "Number is greater than 200"
      else
        echo "Not a number"
      fi
      #fi end if statement
  ```
    - Existem várias condições nativas que podemos usar com **if**.
        - `-e file` para checar se o arquivo existe.
        - `-d file` para checar se o arquivo é um diretório.
        - `-f file` para checar
        - `-r file` para checar se o arquivo pode ser lido.
        - `-w file` para checar se o arquivo pode ser escrito.
        - `-x file` para checar se o arquivo é um executável.
        - `-n string` para checar se a *string* não tem tamanho zero.
        - `-z string` para checar se a *string* tem tamanho zero.
        - Podemos fazer o uso de **[[ ]]** para testar condições de *string*, pois assim ele evita erros como *string*
          vazia.
        - Para checar a lista completa, usar `man 1 test`.
- **Case staments**:
  ```bash
      #!/usr/bin/env bash

      read option

      case $option in
        1) echo "Option $option" ;;
        2) echo "Option $option" ;;
        3) echo "Option $option" ;;
        *) echo "Option $option" ;;
      esac
  ```
- **While**:
  ```bash
      #!/usr/bin/env bash

      myvar=1
      while [ $myvar -le 10]
      do
        echo "$myvar"
        myvar=$(($myvar + 1))
        sleep 0.5
      done
  ```
- **For**:
  ```bash
      #!/usr/bin/env bash

      #for i in 1 2 3 4 5
      #for file in ~/Documents/*
      for i in {1..5} # {1..5} expands to 1 2 3 4 5
      do
        echo "$i"
        sleep 1
      done
  ```
- **Functions**
  ```bash
      #!/usr/bin/env bash

      function hello_world() {
        echo "Hello World!"
      }

      hello_word
  ```
    - *Functions* podem receber argumentos também, o primeiro argumento pode ser acesso através do **$1**. Ex:
      ```bash
        #!/usr/bin/env bash
  
        function hello() {
          echo "Hello $1!"
        }
  
        hello world
        hello Jhon
      ```
- **Arrays**
    - Temos algumas forma de criar *arrays* em bash:
        - `array=(1 2 3 4)` para *array* numérico.
        - `array=('first' 'seconde' ''third)` para *array* de *strings*.
    - Para popular um *array*:
        - Adicionar valor direto no índice, `array[0]=1`.
        - `array+=(5 6)` irá adicionar os valores no final.
        - `array=(0 "${array[@]}")` irá adicionar o valor no começo.
        - `array=("${array[@]}" 0 2 4 6)` irá reescrever com os novos elementos.
    - Para acessar os valores do *array* é semelhante ao declarar por índice.
        - `echo "${array[0]}` irá printar a posição zero do *array*.
        - `echo "${array[-1] }"` irá printar o último elemento.
        - `echo "${array[@]}"` irá printar todos os elementos. Usado também em **for** para iterar em todos os
          elementos.
        - `echo "${array[@:2:3] }"` irá printar 3 elementos partingo do índice 2.
        - `echo "$array=("$@)"` para pegar todos os parâmetros informados ao rodar o *script*.
    - `echo "${#array[0]}"` serve para pegar o tamanho do *array*.
