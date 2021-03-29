# Criando cluster Kubernetes on-line
- Play With Kubernetes (https://labs.play-with-k8s.com/)

## Info
- Tempo limite de utilização 4hs
  
## Master
- Após acessar o site clicar em "+ ADD NEW INSTANCE"
- O proprio aplicativo vai informar os passos para realizar a inicialização do cluster, conforme exemplo abaixo:

 You can bootstrap a cluster as follows:
 1. Initializes cluster master node:
 ```kubeadm init --apiserver-advertise-address $(hostname -i) --pod-network-cidr 10.5.0.0/16```

 2. Initialize cluster networking:
 ```kubectl apply -f https://raw.githubusercontent.com/cloudnativelabs/kube-router/master/daemonset/kubeadm-kuberouter.yaml```

 3. (Optional) Create an nginx deployment:
 ```kubectl apply -f https://raw.githubusercontent.com/kubernetes/website/master/content/en/examples/application/nginx-app.yaml```

- No primeira passo inicializaremos o cluster.
- No segundo passo configuraremos a network do cluster
- No terceiro passo é opcional e pode ser realizado quando todo o cluter já estiver configurado.

### Comando
- No final do primeiro comando vai ser gerado uma URL para utilizarmos na adição dos outros nodes, conforme exempo abaixo:
  
  kubeadm join 192.168.0.22:6443 --token qi5hc0.m5w8shybipdqlinb \
    --discovery-token-ca-cert-hash sha256:c1893ee98ed90d8726dbf457c9ec0e98593a334c49ed7313f81cf23e53854afe

* Esse comando deve ser executado somentes nos nodes que queremos adicionar, não executar no master.

## NODE
- Agora podemos adicionar 1 ou mais nodes clicando em "+ ADD NEW INSTANCE"
- Nesse caso não precisamos rodar os passos informados na tela de abertura, pois já executamos no master.
  
- Para adicionar os nodes no cluster basta rodar o comando:

 ```kubeadm join 192.168.0.22:6443 --token qi5hc0.m5w8shybipdqlinb --discovery-token-ca-cert-hash sha256:c1893ee98ed90d8726dbf457c9ec0e98593a334c49ed7313f81cf23e53854afe```

em todos os nodes que deseja ser inserido no cluster.

- Após isso é só ir no node master e executar o comando  ```kubectl get nodes ``` para ter a informação dos nodes do cluster configurado.