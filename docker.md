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
- `docker exec <CONTAINER> -it bash` para executar comandos dentro do container. Alguns formatos de imagens podem não conter bash e outras ferramentas, nesses casos, trocar bash por sh.
- Usar FLAGS para auxiliar ao rodar o container
    - -d para rodar no background(detached) sem travar o terminal
    - -i para interagir com o container
    - -t faz a alocação de um pseudo terminal
    - -p para mapear a porta do container com o host
    - -u para username quando disponível
    - --name para alterar o nome do container
    - --rm ira remover o mesmo container quando ele parar
## Dockerfile
- Serve para criar uma imagem customizada
- Para criar um dockerfile, basta criar um arquivo com o nome Dockerfile
- Após criado e adicionado os comandos para criação da imagem, fazer o build
    - Usar `docker build .` ou `docker image build .` para criar imagem através do Dockerfile quando estiver no mesmo local do Dockerfile
    - Usar `docker build -t <IMAGE_NAME> .` ou `docker image build -t <IMAGE_NAME> .` para nomear a imagem criada com Dockerfile
    - Usar `docker build -f <SRC_FILE> .` ou `docker image build -f <SRC_FILE> .` para criar imagem em outra pasta
    - Para dar um nome e TAG para a imagem usar `docker build -t NAME:TAG .`
- Para o dockerfile existe uma forma de ignorar arquivos assim como usado gitignore no git. Usar .dockerignore quando houver arquivos a serem ignorados na construção da imagem usando Dockerfile.
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
        - Ex: `COPY foo/bar.txt /containerFolder`
    - `ENV` serve para declaração de variaveis de ambiente. Para acessar vairáveis dentro do Dockerfile, usar $ + nome da variável.
        - Ex: Multiplos valores `ENV FOO=bar XPTO="http://xpto.com"`
        - Ex: Sem o uso do igual(=), desencajado `ENV FOO bar`
    - `EXPOSE` funciona como uma documentação para qual porta o container estará rodando
        - Ex: `EXPOSE 8080`
        - Este comando não altera a porta do container. Para alterar a porta usada no container, usar a flag **-p**
    - `ENTRYPOINT` executa um comando quando o container é iniciado. 
        - Ex: `ENTRYPOINT ["java", "-jar", "myJar.jar"]`
        - Indicado conter apenas um comando pois será executado o ultimo encontrado
        - Este comando pode ser sobreescrito usando --entrypoint \<COMMAND\> ao rodar o container
    - `CMD` executa um comando quando o container é iniciado, similar ao `ENTRYPOINT`
        - Ex: `CMD ["java", "-jar", "myJar.jar"]`
        - Indicado conter apenas um comando pois será executado o ultimo encontrado
        - Este comando pode ser sobreescrito ao rodar o container, adicionando o comando desejado no terminal
    - Exemplo usando um Dockerfile com java e empacotamento em arquivo jar
    ```
    # Openjdk amazon corretto
    FROM amazoncorretto:17.0.3-alpine3.15

    WORKDIR /usr/local/bin/

    # insert you jar here
    COPY ./target/CHANGE_FOR_YOUR_JAR .

    ENTRYPOINT ["java", "-Dspring.profiles.active=prd", "-jar", "CHANGE_FOR_YOUR_JAR.jar"]
    ```

## Docker Compose
- Docker compose é uma ferramenta para definir vários containers e rodar com apenas um comando usando arquivo yaml
- Especificação e lista de comandos [The Compose Specification](https://github.com/compose-spec/compose-spec/blob/master/spec.md)
- Para verificar a versão do docker compose, usar `docker-compose -v`
- **version** é a versão do docker-compose.yaml, ver mais em [Compose versioning](https://docs.docker.com/compose/compose-file/compose-versioning/)
- **build** se informado, usa um arquivo Dockerfile para criar a imagem
- **services** é uma seção para a definição de cada container usado no docker-compose
- **ports** é usado para mapear a porta do container para a porta do host
- **volumes** serve para definir volume, usado da mesmma forma como na CLI usando o *-v* ou *--volume*
- **image** será a imagem usada para o container
- **environment** permite configurar variáveis dentro do container, o mesmo que *-e* na CLI
- **tty** funciona da mesma forma que *-t* através do CLI, abre um pseudo terminal
- **stdin_open** funciona da mesma forma que *-i* através do CLI, habilita interação com o terminal
- Exemplo de docker compose V2, usando uma imagem do mysql versão 8.0.
```
# version was not added following the specification in this date
services:
  db:
    image: mysql:8.0
    container_name: mysqldb
    environment:
      MYSQL_ROOT_PASSWORD: root
    ports:
      - "3306:3306"
```

## Enviar imagem para o docker hub
- Para publicar uma imagem no docker hub, primeiramente precisa ter uma conta
- Para fazer login no seu computador, digitar no terminal `docker login` e inserir suas credenciais
- Usar o comando `docker image push <IMAGE_NAME>` para enviar a imagem
    - Obs. A imagem precisa conter o nome do owner. Ex: fulano/myapp
    - No caso de sua imagem não conter o nome do owner, usar `docker image tag <IMAGE_ID> fulano/myapp` ou recriar a imagem usando build com o nome correto.

## Network
- Habilita a comunicação entre containers
- Um container pode ter uma ou mais networks
- Caso não seja especificado uma, ele usará a padrão
- Para criar uma network via CLI, usar `docker network create <NAME>`
- Para listar networks existentes, usar `docker network ls`
- Para usar a network criada ao rodar um container via CLI, `docker run -it --network <NETWORK> <CONTAINER>`


## Volumes
- Servem para manter os dados quando um container é parado, ao iniciar ele novamente, continuar com os dados gerados anteriomente
- Para criar um volume via CLI, usar `docker volume create <NAME>`
- Para listar volumes, usar `docker volume ls`
- Para usar um volume na criação de container via CLI, usar `docker run -v <VOLUME> <CONTAINER>`