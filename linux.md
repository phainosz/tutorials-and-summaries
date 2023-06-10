# Anotações gerais sobre Linux

## Comandos
- `man` (manual) meio de mostrar ajuda para comandos.
  - `man ls` manual de uso do `ls`.
- `-h` ou `--help` mostra informações de ajuda para comandos.
  - `ls -h` ajuda pra `ls`.
- `pwd` (print working directory) mostra o diretório.
- `ls` (list) lista o conteúdo do diretório.
  - `ls -l` para usar um formato longo de lista.
  - `ls -a` para mostrar arquivos com ponto no começo, arquivos ocultos.
- `cd` (change directory) muda de diretório.
  - `cd Documents` vai pra Documents.
  - `cd ..` volta um diretório.
  - `cd -` vai para o diretório que estava por último.
- `whoami` mostra quem é o usuário logado.
- `clear`  limpa o terminal.
- `cat` serve para mostrar o conteúdo de um arquivo.
- `cp` (copy) copiar um arquivo.
  - `cp file.txt ~/Downloads/` copia o arquivo para diretório especificado.
- `sudo` (super user do) habilita o uso de comandos como root.
- `rm` (remove) serve para remover coisas (arquivos, diretórios).
  - `rm file` remove arquivo com nome file.
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
  - `find /home/ -name*.txt` encontrar qualquer arquivo com extensão txt, partindo do diretório **home**.
- `grep` (global regular expression print) serve para procurar por textos.
  - `cat ~/.profile | grep export` busca a palavra *export* dentro do arquivo.
  - `cat ~/.profile | grep -v export` mostra o conteúdo do arquivo que não tenha a palvra *export* dentro do arquivo.
  - `cat ~/.profile | grep -n export` busca a palavra *export* dentro do arquivo enumerando a linha que se encontra a palavra.
  - `cat ~/.profile | grep -i export` busca a palavra *export* dentro do arquivo de forma a ignorar palavra maiúscula de minúscula.
  - `cat ~/ | grep -r export` busca a palavra *export* dentro do arquivo de forma recursiva que entre nas subpastas.
- `wget` é usado para fazer download usando links.
- `curl` (client url) usado para fazer diferentes tipos de chamdas (http, ftp).
  - `curl -I https://google.com` faz uma chamada GET para o site indicado e traz apenas os headers da resposta.
- `alias` serve para criar apelidos para comandos.
  - `alias la="ls -al` cria apelido para comando indicado.
  - `alias` no terminal n é permante, para tornar permanente, adicionar em **~/.bashrc**.

## Geral
- O diretório que contém as informações de comando do linux se encontra em: **/bin**.
- Para verificar qual versão do linux instalada, usar:
  - `cat /etc/os-release`
  - `hostnamectl`

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
- `chmod +x`
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