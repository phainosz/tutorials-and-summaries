# Anotações gerais sobre Kubernetes

- [Instalação](#instalação)
- [Conceitos](#conceitos)
- [Comandos gerais](#comandos-gerais)
- [Pod](#pod)
- [Config Map](#configmap)

## Instalação
- Windows
 - Usando docker, instalar docker.
 - Ir em configurações -> Kubernetes -> marcar para ativar kubernetes.

## Conceitos
- **Node** é uma máquina física ou virtual onde o kubernetes é instalado para rodar os containers.
- **Cluster** é um agrupamento de nodes.
- **Master** é o node responsável por gerenciar e configurar os múltiplos nodes dentro do cluster.
- **kubectl** kubernetes command line tool é usado para fazer deploy e gerenciar aplicações no cluster.
- **Pod** é como o kubernetes encapsula o container para rodar a instância dentro do Node.
- **YAML** é um formato de arquivo, kubernetes usa *.yml* como arquivo de configuração.
    - Na criação de um arquivo *yml*, existem propriedades comuns e obrigatórias a serem informadas.
    - **apiVersion** é a versão da api usada para criar o objeto.
    - **kind** refere para o tipo do objeto a ser criado.
    - **metadata** são dados sobre o objeto, como *name*, *labels*, etc.

## Comandos gerais
- `kubectl logs <POD>` gera informações de log de um *POD* especificado.
- `kubectl get <pod, node, svc, secret, configmap>` gera informações básicas sobre os componentes.
- `kubectl get <pod, node, svc, secret, configmap> -o wide` gera informações estendidas sobre os componentes.
- `kubectl describe <pod, node, svc, secret, configmap> <NAME>` gera informação específica sobre o componente informado.
- `kubectl create -f <FILENAME>.yml` para criar o tipo do arquivo definido e rodar as configurações.
    - Este comando usado para criar/configurar um recurso que já exista, irá dar erro.
    - O comando `kubctl create` também pode ser usado para criar o recurso de forma imperativa, criar via linha de comando.
- `kubectl apply -f <FILENAME>.yml` para criar ou atualizar um recurso usando as configurações definidas.
- `kubectl delete <pod, node, svc, secret, configmap> <NAME>` deleta o recurso indicando usando o nome do recurso.
- `kubectl delete -f <FILENAME>.yml` deleta o recurso indicando usando o nome do arquivo.

## Pod
- São o menor tipo de unidades de criação dentro do kubernetes.
- Podem ser usados para criar e rodar um simples container usando uma imagem docker por exemplo.
- Ex usando postgres:
```yml
apiVersion: v1
kind: Pod
metadata:
  name: postgres
  labels:
    tier: db-tier
spec:
  containers:
    - name: postgres
      image: postgres
      env:
        - name: POSTGRES_PASSWORD
          value: mysecretpassword
```

## ConfigMap
- Servem para armazenar dados não confidenciais em formato de *chave* *valor*.
- São criados separadamente e referenciados na criação de containers usando por exemplo na criação de *Pods*.
- Ex de criação de **ConfigMap**:
```yml
apiVersion: v1
kind: ConfigMap
metadata: config-example
data:
  #key value example
  mykey: "myvalue"
```
- Ex de como referenciar na criação de containers:
```yml
apiVersion: v1
kind: Pod
metadata:
  name: postgres
  labels:
    tier: db-tier
spec:
  containers:
    - name: postgres
      image: postgres
      env:
        - name: MY_KEY
          valueFrom:
            #get value from ConfigMap
            configMapKeyRef:
              name: config-example
              key: mykey
```