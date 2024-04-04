# Anotações gerais sobre Git

- [Instalação](#instalação)
- [Comandos gerais](#comandos-gerais)
- [Commits](#commits)
- [Branchs](#branchs)
- [Remote](#remote)
- [Stash](#stash)
- [Reverter alterações](#reverter-alterações)
- [SSH](#ssh)

## Instalação
- [Git](https://git-scm.com/)
- Verificar versão com `git version`.

## Comandos gerais
- Para iniciar um repositório `git init`.
- Configurar usuário global `git config --global user.name "<USER>"`.
- Configurar email global `git config --global user.email "<EMAIL>`.
- Ao iniciar um novo repositório, temos a opção de alterar o nome da branch inicial de duas formas:
    - Usando `git init -b <BRANCH_NAME>` ou `git init --initial-branch=<BRANCH_NAME>`.
    - Configurar o git global como `git config --global init.defaultBranch <BRANCH_NAME>`.
- Para clonar um repositório remoto para local `git clone <URL>.git`.

## Commits
- Verificar modificações e arquivos alterados `git status`
- Adicionar itens para a área staged `git add <FILE>` ou `git add .`
    - Arquivos em staged são os que farão parte do próximo commit.
    - Arquivos modificados que não estão na área de staged são chamados de 'Untracked files'.
- Para fazer um commit `git commit -m "<MESSAGE>"`.
    - -m Serve para adicionar a mensagem.
    - Quando precisar alterar a mensagem do último commit sem ter feito o envio para o repositório, utilizar amend.
        - Ex: `git commit --amend -m "<NEW_MESSAGE>"`.
    - Também é possível alterar o último commit com mais arquivos usando o amend, basta adicionar com o add e depois fazer o amend.
    - Quando o commit for com todos os arquivos alterados, pode-se utilizar add + commit `git commit -am "<MESSAGE>"`.
- Após fazer o commit, fazer o envio para o repositório remote com `git push`.
- Para melhorar e facilitar o entendimento e manutenção de código foram criados *commits semânticos*, são formas de padronização de commits em um projeto.
    - Tipos de *commits*:
        - *build*, alterações que afetam dependências e construção do sistema.
        - *ci*, para alterações em arquivos de configuração de ci.
        - *docs*. ajustes em arquivos de documentação.
        - *feat*, novas funcionalidades adicionadas.
        - *fix*, correções de bugs.
        - *perf*, para melhorias de desempenho.
        - *refactor*. mudanças de código mas que não afetam a funcionalidade final.
        - *style*, alterações que não afetam o significado do código, como formatação de código.
        - *test*, usado em testes.
        - *env*, usado em arquivos de configuração.
- Para desfazer commits que foram enviados para o repositório remoto:
    - `git reset --hard HEAD~1` irá voltar para o último commit, podendo alterar o valor para a quantidade de commits anteriores desejado.
    - `git push origin HEAD --force` irá enviar para o repositório remoto as alterações locais que foram feitas.

## Branchs
- Criar nova branch `git checkout -b <NAME>` ou `git switch -c <NAME>`.
- Listar todas as branchs local `git branch`.
- Listar todas as branchs remotas `git branch -r`.
- Listar todas as branchs `git branch -a`.
- Mudar de branch `git checkout <NAME>` ou `git switch <NAME>`.
- Mudar de branch para uma branch remota fazendo o tracking local com remota `git checkout -t <NAME_REMOTE>/<NAME>` ou `git switch -c <NAME> <NAME_REMOTE>/<NAME>`.
    - NAME_REMOTE indica o nome do repositório remoto, podendo ser encontrado através de `git remote -v`.
    - NAME seria o nome da branch.
- Deletar branch local `git branch -D <NAME>`.
- Deletar mais de uma branch com filtro para manter branchs `git branch | grep -v "<NAME_BRANCH_TO_KEEP> | grep -v "<NAME_BRANCH_TO_KEEP> | xargs git branch -D`.
- Deletar branch remota `git branch <NAME_REMOTE> --delete <NAME>`.
- Alterar o nome da branch local, ir para a branch que quer mudar e usar `git branch -m <NEW_NAME>`.
- Alterar o nome da branch remota `git push <NAME_REMOTE> <OLD_BRANCH> <NEW_BRANCH>`.
- Comparar duas branch usando `git diff <BRANCH_1>..<BRANCH_2>`.

## Remote
- Para verificar os repositórios remotos mapeados `git remote -v`.
- Adicionar um repositório remoto `git remote add <NAME> <URL>.git`.
- Renomear o remoto `git remote rename <OLD> <NEW>`.
- Remover o remoto `git remote rm <NAME>`.
- Alterar o endereco remoto `git remote set-url <NAME> <URL>.git`.

## Stash
- É como um arquivo temporário das alterações feitas localmente. Funciona como uma pilha LIFO.
- Para adicionar no stash `git stash`.
- Para adicionar ao stash com nome `git stash push -m <NAME>`.
- Para adicionar novos itens, *untracked files*, o comando é o seguinte:
    - `git stash --include-untracked` ou `git stash -u`
- Para listar itens do stash `git stash list`.
    - Irá retornar algo como `stash@{0}: WIP on something: f2c0c72... My super commit message`.
    - stash@{0} é a identificação do stash na pilha mudando apenas do número {0} para frente.
- Para recuperar o último stash adicionado `git stash pop`.
- Para recuperar por um stash específico `git stash pop stash@{n}`.
    - Usar `git stash list` e trocar n com o número do stash desejado.
- Para remover o primeiro item da lista de stashes `git stash drop`.
- Para remover um stash específico, semelhante ao pop `git stash drop stash@{n}`.

## Reverter alterações
- Quando fazemos alterações e temos essa diferença de arquivos, precisamos entender primeiramente os **stages** presentes no git.
- No **git** temos alguns **stages** e são eles:
    - *Untracked* os arquivos foram criados mas ainda não foram adicionados para o controle do git.
    - *Unmodified* os arquivos não sofreram mudanças.
    - *Modified* é quando houve mudanças no arquivo.
    - *Staged* acontece quando nossas mudanças foram adicionadas ao git com o comando `git add`, podendo ser verificadas com `git status`.
    - *Commit* é o final do ciclo e é onde as mudanças são aplicadas com `git commit` e prontas para serem enviadas para o repositóro remoto.
- Entendendo dos **stages** do **git**, podemos entender como reverter alterações dependendo do **stage** em que essas mudanças se encontram.
- Para remover mudanças que estão como *modified*, usar:
    - `git checkout <FILE>` ou `git restore <FILE>` remove apenas mudanças no arquivo informado.
    - `git checkout .` ou `git restore .`, remove tudo.
- Para remover mudanças que apenas foram adiciondas em *staged* com o comando `git add`, podemos usar:
    - `git reset HEAD <FILE>` ou `git restore --staged <FILE>`, remove apenas mudanças no arquivo informado de *staged*.
        - Com isso, as mudanças saem de *staged* e voltam para *modified*.
- Para remover mudanças que foram feito o *commit*, usar:
    - `git reset --soft HEAD~1`, voltam as mudaças do último *commit* para *staged*.
- Para remover arquivos novos que foram criado, usar:
    - `git clean`, remove novos arquivos que não serão mais usados.
    - Podendo usar as flags:
        - `-d` para remover de forma recursiva nas pastas e subpastas.
        - `-f` para forçar a limpeza.
        - `-n` para mostrar o que será removido, mas não faz a remoção, podendo ser usado para ver previamente os arquivos a serem removidos.

## Tag
- Tags são marcações a serem usadas para identificar um ponto específico do seu software.
- `git tag` é o comando para listar todas as *tags* do seu repositório.
- `git tag -n` lista todas as tags com o nome e descrição da *tag*.
- `git tag <NAME>` para criar uma nova *tag* com o nome informado.
- `git tag -a <NAME>` para criar uma nova *tag* com informações de data, e do usuário que criou a tag.
- `git tag <NAME> -m "<DESCRIPTION>"` para criar uma *tag* com uma descrição.
- Tags assim como as branchs, precisam ser enviadas para o repositório remoto.
    - Usar `git push origin <NAME_TAG>` para enviar a tag local para o remoto.
    - Usar `git push origin --tags` para enviar todas as tags local para o remoto.
- Para remover uma tag local, usar `git tag -d <NAME> `.

## SSH
- Para conectar com repositórios remotos usando o ssh, são necessários alguns passos.
- Github:
    - Linux
        - Checar se existe uma chave SSH presente. No terminal digitar: `ls -al ~/.ssh`.
        - Se algum dos arquivos estiverem presente, *id_rsa.pub*, *id_ecdsa.pub* ou *id_ed25519.pub*, já existe uma chave SSH.
        - Se o passo anterior falhar ou não existir os arquivos, gerar uma nova chave SSH:
            - Usar o comando `ssh-keygen -t ed25519 -C "your_email@example.com`.
            - Em seguida, iniciar o ssh-agent em segundo plano `eval "$(ssh-agent -s)"`.
            - Adicionar a chave SSH no ssh-agent `ssh-add ~/.ssh/id_ed25519`.
        - Para adicionar uma chave SSH existente ou uma nova:
            - Copiar o conteúdo da chave SSH mostrado com o comando `cat ~/.ssh/id_ed25519.pub`.
            - No site do github, abrir configurações > SSH GPG > nova > adicionar título e chave e salvar.
        - Testar conexão com o github, usar o comando `ssh -T git@github.com`.
