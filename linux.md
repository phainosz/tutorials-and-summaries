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
  - **/var/** arquivos variáveis em tamanho e conteúdo conforme o sistema está rodando, exemplos são logs e arquivos temporários.
  - **/root/** diretório para arquivos do usuário root.
  - **/proc/** informações de processos.
- Para criar arquivos de maneira rápida e escrever sem precisar abrir em um editor, podemos usar:
  - `echo linha um > file`
  - `echo linha dois >> file`
  - `echo linha tres >> file`
  - Fazendo isso teremos um arquivo chamada **file** com as 3 linhas que informados.
  - Usando um único *>* irá sobreescrever o conteúdo do arquivo.
  - Usando *>>* irá adicionar no final, concatenar no conteúdo do arquivo.
- Para adicionar novas variáveis no linux, pode ser usados algumas formas diferentes:
  - Adicionar permanentemente, podendo ser adicionado em um dos arquivos: **~/.bashrc** ou **~/bash_profile**
    - Abrir um dos arquivos mencionados e adicionar a variável no arquivo, `export VARIABLE=value`.
    - No terminal digitar o comando `source ~/.bashrc` ou `source ~/.bash_profile` para fazer o load do arquivo no sistema.
    - No caso do **bashrc** não é necessário fazer o load pois este load sempre é feito ao abrir um novo terminal.

## Comandos
- `man` (manual) meio de mostrar ajuda para comandos.
  - `man ls` manual de uso do `ls`.
- `-h` ou `--help` mostra informações de ajuda para comandos.
  - `ls -h` ajuda pra `ls`.
- `pwd` (print working directory) mostra o diretório.
- `ls` (list) lista o conteúdo do diretório.
  - `ls -l` para usar um formato longo de lista.
  - `ls -a` para mostrar arquivos ocultos, que começam com . (ponto) antes do nome.
- `cd` (change directory) muda de diretório.
  - `cd Documents` vai pra Documents.
  - `cd ..` volta um diretório.
  - `cd -` vai para o diretório que estava por último.
- `whoami` mostra quem é o usuário logado.
- `clear`  limpa o terminal.
- `cat` serve para mostrar o conteúdo de um arquivo.
- `head` serve para mostrar as primeiras linhas de um arquivo.
- `tail` serve para mostrar as ultimas linhas de um arquivo.
- `cp` (copy) copiar um arquivo.
  - `cp file.txt ~/Downloads/` copia o arquivo para diretório especificado.
- `sudo` (super user do) habilita o uso de comandos como root.
- `rm` (remove) serve para remover coisas (arquivos, diretórios).
  - `rm file` remove arquivo com nome file.
  - `rm -r folder` remove recursivamente os subdiretórios.
  - `rm -f folder` remove forçando a remoção com arquivos dentro do diretório.
- `adduser` adiciona um novo usuário.
- `which` para encontrar onde um comando se encontra.
  - `which ls` mostra onde se encontra o comando ls.
- `ps` (process status) mostrar os processos rodando.
- `mv` (move or rename) move ou renomeia arquivos.
  - `mv file.txt file2.txt` renomeia o arquivo.
  - `mv file.txt ~/Downloads/` move o arquivo para diretório especificado.
- `mkdir` (make directory) cria um diretório.
- `echo` serve para imprimir algo no terminal.
  - `echo "Oi"` imprimi Oi no terminal.
- `echo "oi" > oi.txt` criar um arquivo com o nome informado e adiciona o texto no arquivo.
  - Se eu repetir o comando, o conteúdo será sobreescrito.
  - Para concatenar, usar `echo "até" >> oi.txt`
- `touch` cria um arquivo.
  - `touch arquivo.txt`
- `find` buscar arquivos.
  - A estrutura de `find` é `find <DIR_TO_START> <OPTIONS> <SEARCH_TERM>`.
    - *DIR_TO_START* é o diretório de origem onde a busca irá começar.
    - *OPTIONS* é dedicado para o arquivo a ser buscado, como nome, tipo, data de criação do arquivo, etc.
  - Tipo de buscas usando `find`:
    - Por nome: `find . -name my-file`, onde **.** é o diretório atual e my-file é o nome do arquivo a ser buscado.
    - Por tipo: `find ~ -type d`, onde **~** é o diretório **home** do usuário logado e d seria para diretórios.
      - **d** diretório.
      - **f** arquivo.
    - Por tamanho do arquivo: `find ~ -size 10M`.
      - c – bytes
      - k – kilobytes
      - M – megabytes
      - G – gigabytes
  - `find /home/ -name *.txt` encontrar qualquer arquivo com extensão txt, partindo do diretório **home**.
  - `find /home/ -name ?.txt` encontrar qualquer arquivo com extensão txt, que tenha um caracter antes do .txt, partindo do diretório **home**.
  - `find /home/ -name [a-z].txt` encontrar qualquer arquivo com extensão txt, que tenha um caracter dentro do carateres informados entre **[ ]** do .txt, partindo do diretório **home**.
  - `find` pode ser usado para encontrar arquivos e executar comandos com os arquivos encontrados.
    - `find ~ -name *.rs -exec cat {} \;` irá encontrar todos os arquivos que tenham extensão .rs e ler o conteúdo dos arquivos encontrados.
      - `-exec` é o que faz executar um comando.
      - Após o `-exec` foi passado o comando `cat`.
      - Os **{}** server como uma lista e recebem/adicionam todos os arquivos encontrados nela.
      - Precisa ter o **\;** ou **';'** para finalizar a expressão.
- `grep` (global regular expression print) serve para procurar por textos.
  - `cat ~/.profile | grep export` busca a palavra *export* dentro do arquivo.
  - `cat ~/.profile | grep -v export` mostra o conteúdo do arquivo que não tenha a palvra *export* dentro do arquivo.
  - `cat ~/.profile | grep -n export` busca a palavra *export* dentro do arquivo enumerando a linha que se encontra a palavra.
  - `cat ~/.profile | grep -i export` busca a palavra *export* dentro do arquivo de forma a ignorar palavra maiúscula de minúscula.
  - `cat ~/.profile | grep -c export` conta quantas vezes a palavra *export* dentro do arquivo.
  - `cat ~/ | grep -r export` busca a palavra *export* dentro do arquivo de forma recursiva que entre nas subpastas.
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
    - Aplicar as mudanças: `souce ~/.bash_profile`
- Usar `sudo passwd USER_NAME` para mudar a senha do usuário informado.
- `df` (disk free) para mostrar a quantidade de espaço livre e usado.
  - `df -H` o `-H` é pra ajudar na forma de apresentação para uma leitura mais humana.
- `tar` é um comando usado para compactar e descompactar arquivos.
  - `tar -cvf file.tar ~/file` irá criar um arquivo tar como nome *file.tar* partindo do arquivo encontrado em *~/file*.
  - `tar -xvf file.tar` irá descompactar um arquivo do tipo tar no diretório atual.
  - Opções disponíveis no comando `tar`:
    - *c* cria um novo arquivo .tar
    - *v* mostra uma descrição do progresso de compactação.
    - *f* nome do arquivo.
    - *z* adiciona o formato de compressão/descompressão **gzip**, usado em arquivo com extensão **.tar.gz**.
- `sed` (stream editor) é um comando usado para modificar o conteúdo de um arquivo ou texto, geralmente adicionando o novo conteúdo em um novo arquivo.
  - Se usarmos `sed s/unix/linux file.txt` irá substituir a primeira palavra de cada linha que tiver *unix* por *linux*.
  - Se usarmos `sed s/unix/linux/2 file.txt` irá substituir a segunda palavra de cada linha que tiver *unix* por *linux*.
  - Se usarmos `sed s/unix/linux/g file.txt` irá substituir todas as palavras *unix* por *linux*.
  - Se usarmos `sed s/unix/linux/g file.txt > file2.txt` irá criar um outro arquivo e substituir todas as palavras *unix* por *linux*.
- `awk` é usado para extrar e printar conteúdos específicos de arquivos.
  - `awk '{print $0}' /etc/passwd` imprimi todo o conteúdo do arquivo, igual ao `cat /etc/passwd`
  - `awk -F: '{ print $1 }' /etc/passwd` imprimi a primeira coluna de cada linha. 
    - `-F` especifica o separador que queira usar por cada coluna, no exemplo `-F:` irá separar cada coluna por **:**.
  - `awk -F: '{ print $1 $7 }' /etc/passwd` imprimi a primeira e sétima coluna de cada linha.
- `sort` é usado para fazer a organização das linhas de um texto de forma ordenada.
  - `sort file.txt` irá ordenar de forma ascendente. 
  - `sort -r file.txt` irá ordenar de forma revertida.
- `strings` é usado para localizar textos legíveis em arquivos binarios, como planilhas do excel, pdf, etc.
  - `string file.xlsx` irá retornar as palavras legíveis para humanos encontradas no arquivo passado.
- `wc` (word count) serve para contas linhas, palavras e characteres de arquivos.
  - `wc file.txt` irá contar linhas, palavras e bytes.
  - `wc -l file.txt` irá contar o número de linhas.
  - `wc -c file.txt` irá contar o número de bytes.
  - `wc -w file.txt` irá contar o número de palavras.
- `traceroute` é usado para inspecionar a rota que o pacote de dados da internet pega até chegar no *host*
  - `traceroute www.google.com` irá mostrar a rota de dados até o host do google.

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
- `env` para listar variáveis do sistema.
- `echo $SHELL` mostra qual *shel* está configurado como padrão.
- `which bash` mostra a localização do *bash*.
- `chmod +x <FILE>.sh` é o comando usado para mudar permissiões de arquivos e diretórios, o *x* libera permissão para execução do arquivo.
  - Arquivos têm 3 tipos de permissões, **r** para ler, **w** para escrever e **x** para executar.
  - Além das permissões dadas, temos quais grupos queremos afetar, **u** para usuário, **g** grupo e **o** outros.
  - Quando executamos o comando `ls -l file` o retorno pode seguir o seguinte formato `-rw-r--r-- 1 ...`. Usuário tem *rw*, grupo *r* e outros *r*.
  - Existe uma forma mais simples de alterar permissões de acesso para arquivos.
    - 1 para executar.
    - 2 para escrever.
    - 4 para ler.
    - `chmod 111 file` dá permissões para executar o arquivos nos 3 grupos(**u,g e o**).
    - Podendo combinar/somar cada um, `chmod 765 file`, usuário pode ler,escrever e executar, grupo pode ler e escrever, outros pode ler e executar.
- `#!/bin/bash` chamado de *shebang*, usado na primeira linha para identificar que o script é do tipo bash script.
- Caso queira criar um script universal, para verificar qual o gerenciador de pacotes, buscar em */etc/*, exemplos: */etc/dnf*, */etc/apt/*.
- Para ler entrada de dados do terminal:
  ```bash
      #!/bin/bash

      echo "Enter your name:"
      read name
      echo "Your name is $name."
  ```
- *Subshell* são comandos realizados de forma apartada. Ex:
  ```bash
      #!/bin/bash

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
      #!/bin/bash

      name="Fulano"

      #has to be double quotes ("). Single quotes would print the name of the variable and not the value.
      echo "Hello $name"
    ```
  - Variáveis inseridas através de comandos:
    ```bash
      #!/bin/bash

      #use commands as variables
      files=$(ls)

      echo $files
    ```
- **Math**:
  - Bash usa expressões matemáticas de forma diferente.
  - Para fazer cálculos em bash, usar: `expr`
    - Soma: `expr 10 + 10`
    - Subtração: `expr 10 - 10`
    - Divisão: `expr 10 / 10`
    - Multiplicação: `expr 10 \* 10`
- **If statements**:
  ```bash
      #!/bin/bash
      
      mynum=200

      #eq - equal
      #ne - not equal
      #gt - greater tha
      #lt - less than
      #ge - greater than or equal
      #le - less than or equal
      #more conditions check man test
      if [$mynum -eq 200]
      then
        echo "Condition is true."
      else
        echo "Condition is false."
      fi
      #fi end if statement
  ```
  - Para verificar se um arquivo existe em um diretório: `if [-f ~/file]`
- **Exit codes**:
  - São uma forma de verificar se o u último comando foi executado com sucesso.
  - Se eu rodar qualquer comando, para verificar se ele teve sucesso, verificar o valor de `$?`
  - Ex: `sudo dnf install notexist` e depois `echo $?`. Em caso de sucesso, o retorno será 0, qualquer erro terá o código diferente de 0.
- **While**:
  ```bash
      #!/bin/bash

      myvar=1
      while [ $myvar -le 10]
      do
        echo $myvar
        myvar=$(($myvar + 1))
        sleep 0.5
      done
  ```
- **For**:
  ```bash
      #!/bin/bash

      #for i in 1 2 3 4 5
      #for file in ~/Documents/*
      for i in {1..5}
      do
        echo $i
        sleep 1
      done
  ```
- **Functions**
  ```bash
      #!/bin/bash

      function hello_world() {
        echo "Hello World!"
      }

      hello_word
  ```
- **Case staments**:
  ```bash
      #!/bin/bash

      read option

      case $option in
        1) echo "Option $option";;
        2) echo "Option $option";;
        3) echo "Option $option";;
        *) echo "Option $option"
      esac
  ```
- **Arguments**:
  ```bash
      #!/bin/bash

      #./script.sh first
      #echo Entered argument: first
      echo "Entered argument: $1"
  ```