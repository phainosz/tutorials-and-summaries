# Anotações gerais sobre docker

## Intalação
- [Docker](https://docs.docker.com/get-docker/)
- Verificar versão com `docker version`

## Comandos gerais
- Para verificar comandos de ajuda para o docker usar `docker --help`
    * Pode ser utilizado junto com comando especificos, ex: `docker container --help`
- Comandos antigos eram utilizados sem especificar uma subcategoria, atualmente existe uma forma mais nova
    * Antigo: `docker ps`
    * Novo: `docker container ls`
    * Serve para outros comandos, olhar doc ou usar `docker COMANDO --help`
- `docker ps` OU `docker container ls` exibe os containers rodando
- `docker ps-a` OU `docker container ls -a` exibe todos os containers
- `docker rm NAME_CONTAINER` OU `docker rm ID_CONTAINER` remove o container escolhido
- `docker run NOME_CONTAINER` OU `docker container run NAME_CONTAINER` roda o container
- `docker start ID_CONTAINER` OU `docker container run ID_CONTAINER` roda o container
- `docker stop NAME_CONTAINER` OU `docker container stop NAME_CONTAINER` parar o container
- `docker exec NAME_CONTAINER` OU `docker container exec NAME_CONTAINER` executar um container ou comando para o container
- `docker images` OU `docker image ls` mostra detalhes de imagens local
- `docker images inspect ID_IMAGEM` OU `docker image inspect ID_IMAGEM` mostra detalhes da imagem informada
- `docker cp SRC_ORIGEM SRC_DESTINO` OU `docker container cp SRC_ORIGEM SRC_DESTINO` para copiar arquivos, podendo ser do container para o pc ou vice versa
- Usar FLAGS para auxiliar ao rodar o container
    * -d para rodar no background sem travar o terminal
    * -i para interagir com o container
    * -t faz a alocação de um pseudo terminal

## Dockerfile
- Serve para criar uma imagem customizada
- Para criar um dockerfile, basta criar um arquivo com o nome Dockerfile
- Após criado e adicionado os comandos para criação da imagem, fazer o build
    - Usar `docker build .` OU `docker build -f SRC_DOCKERFILE .`
    - Para dar um nome e TAG para a imagem usar `docker build -t NOME:TAG .`
- Instruções para o Dockerfile
    - INSTRUCAO argumento, este é o padrão para adicionar os comandos
    - `FROM` é a primeira instrução e é ela que informa qual a imagem iremos utilizar
        - Ex: `FROM openjdk:latest`
        
## Docker Compose