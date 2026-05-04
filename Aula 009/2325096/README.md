# TF - Aula 09: Fundamentos de Kubernetes (K8s)

## Questão 1: Arquitetura e Componentes

### a)
O Control Plane (Master) é o componente responsável por gerenciar todo o cluster Kubernetes. Ele controla o estado do cluster, agenda workloads, monitora recursos e garante que o estado desejado seja mantido.

Um componente chave do Control Plane é o etcd, que funciona como o banco de dados distribuído do Kubernetes, armazenando o estado e as configurações do cluster.

### b)
O principal software que roda nos Worker Nodes é o kubelet.

O kubelet é o agente responsável por garantir que os Pods definidos estejam rodando corretamente no Node, monitorando seu estado e mantendo o estado desejado.

---

## Questão 2: O Pod

### a)
Um Pod pode conter múltiplos contêineres quando esses contêineres precisam trabalhar juntos como uma única unidade lógica.

Esses contêineres compartilham:
- a mesma rede (mesmo IP)
- o mesmo namespace
- volumes/storage (quando configurados)

Isso permite que eles se comuniquem facilmente.

### b)
Criar Pods diretamente em produção é inadequado porque Pods sozinhos não possuem gerenciamento automático.

Se um Pod falhar, ele não será recriado automaticamente.

Por isso, em produção usamos Deployments, pois eles garantem:
- self-healing
- escalabilidade
- atualizações
- gerenciamento do estado desejado

---

## Questão 3: Manifesto YAML

Os quatro campos obrigatórios na raiz de um manifesto Kubernetes são:

- apiVersion
- kind
- metadata
- spec

---

## Questão 4: Deployment

Arquivo: `deployment.yaml`

---

## Questão 5: Service

Arquivo: `service.yaml`

---

## Tarefa Prática Integrada

Quando o usuário acessa a aplicação pelo navegador, a requisição segue o seguinte fluxo:

1. A requisição chega ao Node do cluster pela porta NodePort (NodeIP:30080).
2. O Service `web-service-tf09` intercepta essa requisição.
3. O Service usa o campo selector (`app: web-tf09`) para identificar quais Pods estão aptos a receber o tráfego.
4. O kube-proxy é responsável por rotear o tráfego do Service para um dos Pods ativos.
5. A requisição é encaminhada para um dos Pods gerenciados pelo Deployment `nginx-deploy-tf09`.
6. Dentro do Pod, o contêiner Nginx recebe a requisição na porta 80.

---

## Passo a passo para subir o ambiente

### 1. Iniciar o Minikube

```bash
minikube start