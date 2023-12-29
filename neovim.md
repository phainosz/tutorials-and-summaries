# Anotações gerais sobre Neovim

## Instalação
- [Neovim](https://github.com/neovim/neovim/wiki/Installing-Neovim)


## Geral
- `nvim file.txt` abre *file.txt* e se não existir cria o arquivo.
- Para executar comandos bash no neovim, entrar em *command mode* e digitar `! <COMMAND>`.
  - Ex: `! ls $HOME`

## Motions

### Normal Mode
- `h` move o cursor para a esqueda.
- `j` move o cursor para a baixo.
- `k` move o cursor para a cima.
- `l` move o cursor para a direita.
- `i` entra em *Insert mode* no local onde o cursor está.
- `a` entra em *Insert mode* no final da palavra onde o cursor está.
- `o` entra em *Insert mode* na próxima linha onde o cursor está.
- `I` entra em *Insert mode* no início da linha onde o cursor está.
- `O` entra em *Insert mode* na linha acima onde o cursor está.
- `A` entra en *Insert mode* no final da linha onde o cursor está.
- `u` desfaz o que foi feito.
- `Ctrl + R` volta o que foi desfeito. 
- `0` move o cursor para o início da linha.
- `_` move o cursor para o início do texto na linha.
- `$` move o cursor para o fim da linha.
- `v` entra no *Visual mode* e seleciona um caractere.
  - podendo combinar com os movimentos usando `h`,`j`,`k` ou `l`.
- `dd` deleta a linha inteira. Podendo ser usado como recortar linha.
- `yy` copia a linha inteira.
- `p` para colar o que foi copiado. Quando copia a linha inteira
- `P` para copiar o que foi copiado na linha acima do cursor.
- `cw` delete próxima palavra e entra em *insert mode*.
  - Podendo ser combinado com outros movimentos horizontais.
  - `cb` deleta palavra anterior do cursor e entra em *insert mode*.
- `cc` deleta tudo da linha mas mantém a linha e entra em *Insert mode*.
- `D` deleta o que está para a frente do cursor.
- `C` deleta o que está para a frente do cursor e entra em *Insert mode*.
- `w` movimenta o cursor para frente pulando por palavras.
- `W` movimenta o cursor para frente pulando por palavras considerando apenas espaço como pulo.
- `b` movimenta o cursor para trás pulando por palavras.
- `B` movimenta o cursor para trás pulando por palavras considerando apenas espaço como pulo.
- `H` move o curso para o topo da tela.
- `M` move o curso para o meio da tela.
- `L` move o curso para o final da tela.
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
  - `;` vai para o próximo símbolo encontrado na linha.
  - `,` vai para o símbolo anterior encontrado na linha.
  - Usando `F` vai para o sentido contrário.
- `gg` vai para o começo do arquivo.
- `G` vai para o final do arquivo.
  - Podendo combinar linhas com `G` para ir para a linha específica,
  - Exemplo: `10G` vai para a linha 10.
- `==` identa a linha que o cursor está.
- `x` deleta a letra em que o cursor está.
- `X` deleta a letra anterior em que o cursor está.
- `J` junta a próxima linha com a atual.
- `cc` ou `S`. deleta linha inteira e entra em *insert mode*
- `}` vai para o próximo paragráfo.
- `{` vai para o paragráfo anterior.
- `zz` para centralizar o cursor.
- `zt` para posicionar o cursor no topo da tela.
- `zb` para posicionar o cursor no final da tela.
- `>>` identar linha para direita.
- `<<` identar linha para esquerda.
- `1k` sobe uma linha. Podendo ser trocado o número com a quantidade de linhas desejadas.
- `1j` desce uma linha. Podendo ser trocado o número com a quantidade de linhas desejadas.
- `Ctrl + d` para mover a tela meia página para baixo.
- `Ctrl + u` para mover a tela meia página para cima.
- `Shift + Ctrl + c` para copiar o texto selecionado usando *visual mode*.
- `Shift + Ctrl + v` para colar o texto normal.

### Command Mode
- `:` execução de comandos.
- `:w` para salvar o arquivo sem sair.
- `:wq` para salvar e sair do arquivo.
- `/` é o comando para buscar algo no arquivo.
  - Combinar com o que quer ser buscado.
  - Pressionar enter.
  - `n` para mover para a próxima ocorrência.
  - `N` para voltar para ocorrência anterior.
- Alterar palavra usando o *command mode*.
  - Digitar `:%s/word/word2` irá alterar word para word2.
- `map <C-a> ggVG` mapeia um comando para um atalho desejado. No exemplo, vai para o ínicio do arquivo, entra em *modo visual* e vai para o fim do arquivo, mapeia para *Ctrl a*.

### Insert Mode
- `esc` para sair do mode e ir para *Normal mode*.

### Visual Mode
- `d` para deletar o que foi selecionado.
- `y` copia o que foi selecionado, termo usado é chamado de *yanking*.
  - `p` para colar o que foi copiado no final o que foi copiado usanod `v`.
  - `P` para colar no início da linha o que foi copiado usanod `v`.
- `c` deleta a palavra selecionada e entra em *Insert mode*.
- `=` identa toda o conteúdo selecionado.
- Selecionar um texto e apertar `u` irá alterar a seleção para minúsculo.
- Selecionar um texto e apertar `U` irá alterar a seleção para maiúculo.
- `aw` selecionar uma palavra.
- `a(` selecionar bloco entre *()*.
- `a{` selecionar bloco entre *{}*
- `at` selecionar bloco entre *<>*. 

### Visual Mode Block
- Para entrar em neste modo, usar `Ctrl + v`.
- Usado para realizar ações em múltiplas linhas.
