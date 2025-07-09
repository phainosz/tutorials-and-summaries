# Anotações gerais sobre Kubernetes

- [Instalação](#instalação)
- [Conceitos](#conceitos)
- [Comandos gerais](#comandos-gerais)
- [Pod](#pod)
- [Config Map](#configmap)
- [Secrets](#secrets)
- [Replication Controller e Replica Set](#replication-controller-e-replica-set)
- [Deployment](#deployment)
- [Service](#services)

## Instalação

- Windows
    - Usando docker, instalar docker:
        - Ir em configurações -> Kubernetes -> marcar para ativar kubernetes.
    - [Minikube](https://minikube.sigs.k8s.io/docs/start/]):
        - `winget install minikube`
        - Minikube facilita no processo de instalação e uso local.
- Linux
    - [Minikube](https://minikube.sigs.k8s.io/docs/start/]):
      ```
        curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
        sudo install minikube-linux-amd64 /usr/local/bin/minikube
      ```

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

- `kubectl logs <POD_NAME>` gera informações de log de um **Pod** especificado.
    - `kubectl logs -f <POD_NAME>` mostra logs do *pod* informado em tempo real.
- `kubectl get <RESOURCE>` gera informações básicas sobre os componentes.
    - resources: *svc*, *deployments*, *pods*, *configmaps*, etc.
    - `kubectl get pods --all-namespaces` lista todos os *pods* de todos os *namespaces*.
    - `kubectl get pods -n <NAMESPACE>` lista todos os *pods* do *namespace* informado.
- `kubectl get <RESOURCE> -o wide` gera informações estendidas sobre os componentes.
    - `kubectl get pods <POD_NAME> -n <NAMESPACE>`.
- `kubectl describe <RESOURCE> <RESOIRCE_NAME>` gera informação específica sobre o componente informado.
    - `kubectl describe pods <POD_NAME> -n <NAMESPACE>`.
- `kubectl create -f <FILENAME>.yml` para criar o tipo do arquivo definido e rodar as configurações.
    - Este comando usado para criar/configurar um recurso que já exista, irá dar erro.
    - O comando `kubctl create` também pode ser usado para criar o recurso de forma imperativa, criar via linha de
      comando.
- `kubectl get all` mostra todos o recursos do *namespace* atual.
    - `kubectl get all -n <NAMESPACE>` mostra todos o recursos do *namespace* informado.
- `kubectl get namespaces` lista todos os *namespaces* do *cluster*.
- `kubectl top pods` mostra métricas dos pods, incluindo CPU e uso de memória.
    - Podendo ser usado com outros recursos ou um recurso em específico: `kubectl top pod <POD_NAME>`.
- `kubectl cluster-info` mostra informações sobre o *cluster*.
- `kubectl apply -f <FILENAME>.yml` para criar um recurso usando as configurações definidas.
- `kubectl delete <RESOURCE> <NAME>` deleta o recurso indicando usando o nome do recurso.
- `kubectl delete -f <FILENAME>.yml` deleta o recurso indicando usando o nome do arquivo.
- `kubectl replace -f <FILENAME>.yml` substitui um recurso com base em configurações antigas.
- `kubectl explain <RESOURCE>` dá uma breve descrição sobre o recurso especificado.
- `kubectl edit <RESOURCE> <NAME>` usado para editar o arquivo usado para configura este recurso com novas
  configurações.

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

- São recursos com funcionalidades e propósitos iguais, um sendo a versão antiga e o outro a mais recente,
  sucessivamente.
- Servem para manter de forma estável **Pods** rodando em qualquer momento e a quantidade especificada.
- **ReplicaSet** garante que a quantidade de **Pods** configuradas estejam sempre rodando, entretanto, **Deployment** é
  um recurso de nível acima que gerenciam **ReplicaSet** e provisionam de forma declarativa a criação e atualização de *
  *Pods** e outras configurações úteis. É recomendado o uso de **Deployments** ao invés de **ReplicaSet**.
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

## Services

- Habilitam conexão entre **Pods** dentro do **Cluster**.
- Existem 4 *types* na configuração de **Services**: *ClusterIP* (default), *NodePort*, *LoadBalancer* e *ExternalName*.
- *ClusterIP* o **Service** não é exposto para fora do **Cluster** mas pode ser usado internamente.
- *NodePort* o **Service** é exposto para fora do **Cluster** e pode ser usado externamente com a porta estática do
  *Node* mais a porta configurada no *NodePort*, *<NODE_IP>:<NODE_PORT>*.
- *LoadBalancer* também é exposto para fora do **Cluster** que será usado conforme o *Load Balancer* disponibilizado
  pelo provedor que for fornecido.
- *ExternalName* é exposto para fora do **Cluster**, mapeia o **Service** com um *DNS* pré definido.
- Ex *NodePort*:

```yml
apiversion: v1
kind: Pod
metadata:
  name: postgres-pod
  selector:
    app: postgres-pod
spec:
  containers:
    - name: postgres
      image: postgres
      ports:
        - containerPort: 80
          name: postgres-port

---

apiVersion: v1
kind: Service
metadata:
  name: myapp-service
spec:
  type: NodePort
  #in order to use the targetPort to bind with the Pod, we need to select the Pod labels using selector
  selector:
    app: postgres-pod
  ports:
    #port is the port of the service
    - port: 80
      #targetPort is the port of the container running we want to bind
      #targetPort can referece the name defined in a Pod port
      targetPort: 80 #or targetPort: postgres-port
      #nodePort is the port we want to expose outside the cluster
      #nodePort has a range of 30000-32767
      nodePort: 30008
```