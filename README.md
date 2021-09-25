# valyria-notes

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

cd /tmp
curl -LO https://github.com/derailed/k9s/releases/download/v$K9S_VERSION/k9s_Linux_x86_64.tar.gz
tar zxvf k9s_Linux_x86_64.tar.gz
sudo cp k9s /usr/local/bin/

# OR: sudo snap install k9s

curl -o kubectl -L https://dl.k8s.io/release/v$K8S_CLI_VERSION/bin/linux/amd64/kubectl
chmod +x kubectl
sudo mv kubectl /usr/local/bin

# OR: sudo snap install kubectl --classic

curl -s https://fluxcd.io/install.sh | sudo bash

export GITHUB_TOKEN=<my-token>
flux bootstrap github \
  --owner=avnes \
  --repository=valyria-flux \
  --path=clusters/${K8S_CLUSTER_NAME} \
  --personal

curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh

# OR: sudo snap install helm --classic
```

## TODO

The purpose is to use automation to install and configure as much as possible. I also want to become less dependent on using microk8s as the k8s implementation.

- DONE: Increase RAM from 2GB to 8GB.
- DONE: Increase vCPU from 1 to 2 cores.
- DONE: Refactor some git repo names
- Automate installation of Flux CD
- Automate installation of Traefik with Flux CD
- Automate installation of Fluentd with Flux CD
- Automate installation of (Bitnami) MetalLB with Flux CD
- Automate installation of Kubernetes Dashboard with Flux CD
- Automate installation of Prometheus Blackbox Exporter with Flux CD
- Automate installation of kube-prometheus-stack with Flux CD
- Automate installation and configuration of microk8s.
- Automate installation of helm, kubectl, k9s and potentially other CLI tools instead of using the ones included with microk8s.
- Look into Longhorn as storage solution
- Look into Loki for accessing logs in Grafana

## CheatSheet virsh

```bash
sudo virsh list --all       # List all domains
sudo virsh stop dragonlord  # Stop one domain
sudo virsh edit dragonlord  # Open an editor and tweak the VM settings
sudo virsh start dragonlord # Start one domain
```
