# Anotações gerais sobre Docker

## Intalação
- [Docker](https://docs.docker.com/get-docker/)
- Verificar versão com `docker version`

## Comandos gerais
- Para verificar comandos de ajuda para o docker usar `docker --help`
    - Pode ser utilizado junto com comando especificos, ex: `docker container --help`
- Comandos antigos eram utilizados sem especificar uma subcategoria, atualmente existe uma forma mais nova
    - Antigo: `docker ps`
    - Novo: `docker container ls`
    - Serve para outros comandos, olhar doc ou usar `docker <COMANDO> --help`
- `docker ps` ou `docker container ls` exibe os containers rodando
- `docker ps-a` ou `docker container ls -a` exibe todos os containers
- `docker rm <CONTAINER_ID>` ou `docker container rm <CONTAINER_ID>` remove o container escolhido
- `docker container prune` para remover todos os containers parados
- `docker run <IMAGE>` ou `docker container run <IMAGE>` roda o container
- `docker start <CONTAINER_ID>` ou `docker container run <CONTAINER_ID>` roda o container
- `docker stop <CONTAINER_ID>` ou `docker container stop <CONTAINER_ID>` parar o container
- `docker exec <CONTAINER_ID>` ou `docker container exec <CONTAINER_ID>` executar um container ou comando para o container
    - Usado em conjunto com os comandos -it para realizar comando dentro do container
- `docker container logs <CONTAINER_ID>` para ver os logs do container informado
- `docker pull <IMAGE>` ou `docker image pull <IMAGE>` faz o download da imagem
- `docker images` ou `docker image ls` mostra detalhes de imagens local
- `docker images inspect <IMAGE>` ou `docker image inspect <IMAGE>` mostra detalhes da imagem informada
- `docker cp <SOURCE> <DEST>` ou `docker container cp <SOURCE> <DEST>` para copiar arquivos, podendo ser do container para o pc ou vice versa
- Usar FLAGS para auxiliar ao rodar o container
    - -d para rodar no background(detached) sem travar o terminal
    - -i para interagir com o container
    - -t faz a alocação de um pseudo terminal
    - -p para mapear a porta do container com o host
    - -u para username quando disponível
    - --name para alterar o nome do container

## Dockerfile
- Serve para criar uma imagem customizada
- Para criar um dockerfile, basta criar um arquivo com o nome Dockerfile
- Após criado e adicionado os comandos para criação da imagem, fazer o build
    - Usar `docker build .` ou `docker build -f <SRC_DOCKERFILE> .`
    - Para dar um nome e TAG para a imagem usar `docker build -t NOME:TAG .`
- Instruções para o Dockerfile
    * \# Adiciona comentários dentro do Dockerfile
    - INSTRUCAO argumento, este é o padrão para adicionar os comandos
    - `FROM` é uma instrução obrigatória e é ela que informa qual a imagem iremos utilizar
        - Ex: `FROM openjdk:latest`
    - `RUN` executa qualquer comando nas camadas de criação da imagem
        - Ex: `RUN apt-get update` ou `RUN npm install`
    - `WORKDIR`define um diretório de trabalho
        - EX: `WORKDIR /app`
    - `COPY` basicamente copia arquivos locais para o container
        - Ex: `COPY myfolder/file.txt /containerFolder`
    - `ENV` serve para declaração de variaveis de ambiente
        - Ex: Multiplos valores `ENV MY_ENV=http://bla.com MY_ENV2="My Env"`
        - Ex: Sem o uso do igual(=), desencajado `ENV MY_ENV http://bla.com`
    - `EXPOSE` funciona como uma documentação para qual porta o container estará rodando
        - Ex: `EXPOSE 8080`
        - Este comando não altera a porta do container. Para alterar a porta usada no container, usar a flag **-p**
    - `ENTRYPOINT` executa um comando quando o container é iniciado.
        - Ex: `ENTRYPOINT ["java" "-jar" "meuJar.jar"]`
        - Este comando pode ser sobreescrito usando --entrypoint \<COMMAND\> ao rodar o container
        
## Docker Compose