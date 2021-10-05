# microk8s notes

```bash
K8S_VERSION=1.21
K8S_CLI_VERSION=1.21.5
K8S_CLUSTER_NAME=valyria

K9S_VERSION=0.24.15

sudo snap install microk8s --classic --channel=${K8S_VERSION}
microk8s status --wait-ready
microk8s kubectl get nodes
microk8s enable dns storage
microk8s enable metallb:192.168.1.240/24
microk8s config > ~/.kube/${K8S_CLUSTER_NAME}.config
KUBECONFIG=~/.kube/${K8S_CLUSTER_NAME}.config; export KUBECONFIG
```
