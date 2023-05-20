# Anotações gerais sobre Neovim

## Instalação
- [Neovim](https://github.com/neovim/neovim/wiki/Installing-Neovim)

## Motions

### Normal Mode
- `h` move o cursor para a esqueda.
- `j` move o cursor para a baixo.
- `k` move o cursor para a cima.
- `l` move o cursor para a direita.
- `:` execução de comandos.
- `i` entra em *Insert mode* no local onde o cursos está.
- `:w` para salvar o arquivo sem sair.
- `:wq` para salvar e sair do arquivo.
- `a` entra em *Insert mode* no final da palavra onde o cursos está.
- `o` entra em *Insert mode* na próxima linha onde o cursor está.
- `I` entra em *Insert mode* no início da linha onde o cursos está.
- `O` entra em *Insert mode* na linha acima onde o cursos está.
- `A` entra en *Insert mode* no final da linha onde o cursos está.
- `u` desfaz o que foi feito.
- `r` volta o que foi desfeito. 
- `0` move o cursos para o início da linha.
- `$` move o cursor para o fim da linha.
- `v` entra no *Visual mode* e seleciona um caractere.
  - podendo combinar com os movimentos usando `h`,`j`,`k` ou `l`.
- `dd` deleta a linha inteira. Podendo ser usado como recortar linha.
- `yy` copia a linha inteira.
- `p` para colar o que foi copiado. Quando copia a linha inteira
- `P` para copiar o que foi copiado na linha acima do cursor.
- `cc` deleta tudo da linha mas mantém a linha e entra em *Insert mode*.
- `D` deleta o que está para a frente do cursor.
- `C` deleta o que está para a frente do cursor e entra em *Insert mode*.
- `w` movimenta o cursor para frente pulando por palavras.
- `W` movimenta o cursor para frente pulando por palavras considerando apenas espaço como pulo.
- `b` movimenta o cursor para trás pulando por palavras.
- `B` movimenta o cursor para trás pulando por palavras considerando apenas espaço como pulo.
- `dw` deleta a próxima palavra.
- `d2w` deleta as duas próximas palavras.
- `diw` deleta a palavra em que o cursor está em cima.
- `ciw` deleta a palavra em que o cursor está em cima e entra em *Insert mode*.
- `e` vai para o final da palavra.
- `yiw` copia a palavra em que o cursor está em cima.
- `t` move o cursor para frente antes da palvra/símbolo buscado.
  - Ex: `t*` move o cursor para o até * encontrado.
- `t` move o cursor para trás antes da palvra/símbolo buscado. 
- `f` move o cursor para frente na palvra/símbolo buscado.
  - Ex: `f*` move o cursor para no * encontrado.
- `f` move o cursor para trás na palvra/símbolo buscado.
- `gg` vai para o começo do arquivo.
- `G` vai para o final do arquivo.
  - Podendo combinar linhas com `G` para ir para a linha específica,
- `==` identa a linha que o cursor está.
- `/` é o comando para buscar algo no arquivo.
  - Combinar com o que quer ser buscado.
  - Pressionar enter.
  - `n` para mover para a próxima ocorrência.
  - `N` para voltar para ocorrência anterior.
- `x` deleta a letra em que o cursor está.
- `X` deleta a letra anterior em que o cursor está.

### Insert Mode
- `esc` para sair do mode e ir para *Normal mode*.

## Visual Mode
- `d` para deletar o que foi selecionado.
- `y` copia o que foi selecionado, termo usado é chamado de *yanking*.
  - `p` para colar o que foi copiado no final o que foi copiado usanod `v`.
  - `P` para colar no início da linha o que foi copiado usanod `v`.
- `c` deleta a palavra selecionada e entra em *Insert mode*.
- `=` identa toda o conteúdo selecionado.