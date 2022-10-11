# Anotações gerais sobre Kubernetes

- [Instalação](#instalação)
- [Conceitos](#conceitos)
- [Comandos gerais](#comandos-gerais)
- [Pod](#pod)
- [Config Map](#configmap)
- [Secrets](#secrets)
- [Replication Controller e Replica Set](#replication-controller-e-replica-set)
- [Deployment](#deployment)

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
- `kubectl logs <POD>` gera informações de log de um **Pod** especificado.
- `kubectl get <RESOURCE>` gera informações básicas sobre os componentes.
- `kubectl get <RESOURCE> -o wide` gera informações estendidas sobre os componentes.
- `kubectl describe <RESOURCE> <NAME>` gera informação específica sobre o componente informado.
- `kubectl create -f <FILENAME>.yml` para criar o tipo do arquivo definido e rodar as configurações.
    - Este comando usado para criar/configurar um recurso que já exista, irá dar erro.
    - O comando `kubctl create` também pode ser usado para criar o recurso de forma imperativa, criar via linha de comando.
- `kubectl apply -f <FILENAME>.yml` para criar um recurso usando as configurações definidas.
- `kubectl delete <RESOURCE> <NAME>` deleta o recurso indicando usando o nome do recurso.
- `kubectl delete -f <FILENAME>.yml` deleta o recurso indicando usando o nome do arquivo.
- `kubectl replace -f <FILENAME>.yml` substitui um recurso com base em configurações antigas.
- `kubectl explain <RESOURCE>` dá uma breve descrição sobre o recurso especificado.
- `kubectl edit <RESOURCE> <NAME>` usado para editar o arquivo usado para configura este recurso com novas configurações.

## Pod
- São o menor tipo de unidades de criação dentro do kubernetes.
- Podem ser usados para criar e rodar um simples containers usando uma imagem docker por exemplo.
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
- São criados separadamente e referenciados na criação de containers usando por exemplo na criação de **Pods**.
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
      #it's possible to use envFrom instead of env. The difference is that envFrom loads all the keys as environment variables.
      env:
        - name: MY_KEY
          valueFrom:
            #get value from ConfigMap
            configMapKeyRef:
              name: config-example
              key: mykey
```

## Secrets
- Servem para armazenar dados confidenciais em formato de *chave* *valor*.
- Ex:
```yml
apiVersion: v1
kind: Secret
metadata:
  name: mysecret
type: Opaque
data:
  key: value
```
- Ex de como referencia em um **Pod**:
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
            secretKeyRef:
              name: mysecret
              key: key
```

## Replication Controller e Replica Set
- São recursos com funcionalidades e propósitos iguais, um sendo a versão antiga e o outro a mais recente, sucessivamente.
- Servem para manter de forma estável **Pods** rodando em qualquer momento e a quantidade especificada.
- **ReplicaSet** garante que a quantidade de **Pods** configuradas estejam sempre rodando, entretanto, **Deployment** é u recurso de nível acima que gerenciam **ReplicaSet** e provisionam de forma declarativa a criação e atualização de **Pods** e outras configurações úteis. É recomendado o uso de **Deployments** ao invés de **ReplicaSet**.
- Ex de criação de **ReplicaSet**
```yml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: myapp-rs
  labels:
    app: myapp
#specification for ReplicaSet
spec:
  #the section template is the same as creating a Pod only without apiVersion and kind section
  template:
    metadata:
      name: postgres
      labels:
        app: myapp
    #specification for Pod
    spec:
      containers:
        - name: postgres
          image: postgres
  replicas: 3
  #selector is used in ReplicaSet, for ReplicationController the items bellow is not configured
  selector:
    #Pod label and matchLabels must be the same
    matchLabels:
      app: myapp
```

## Deployment
- Configura de forma declarativa criação e atualização de **Pods** e **ReplicaSets**.
- Funciona de forma similiar, porém engloba a criação de **ReplicaSet** através da criação do **Deployment**.
- A diferença está nas funcionalidades a mais que **Deployment** agrega, como por exemplo, *rollout* e *rollback*.
- Ex:
```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-deployment
  labels:
    app: myapp
spec:
  template:
    metadata:
      name: postgres
      labels:
        app: myapp
    spec:
      containers:
        - name: postgres
          image: postgres
  replicas: 3
  selector:
    matchLabels:
      app: myapp
```