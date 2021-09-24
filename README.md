# valyria-notes

´´´bash
KUBE_VERSION=1.21
K9S_VERSION=0.24.15

sudo snap install microk8s --classic --channel=${KUBE_VERSION}
microk8s status --wait-ready
microk8s kubectl get nodes
printf "alias kubectl='microk8s kubectl'" >> ~/.bash_aliases
source ~/.bash_aliases
microk8s enable dns storage dashboard fluentd helm3
microk8s enable metallb:192.168.1.240/24
microk8s enable traefik
microk8s config > ~/.kube/valyria.config
KUBECONFIG=~/.kube/valyria.config; export KUBECONFIG

curl -LO https://github.com/derailed/k9s/releases/download/v${K9S_VERSION}/k9s_Linux_x86_64.tar.gz
tar zxvf k9s_Linux_x86_64.tar.gz
sudo cp k9s /usr/local/bin/
´´´

Notes: fluentd stack is not starting due to insufficient memory. I need more juice :)
