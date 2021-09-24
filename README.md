# valyria-notes

```bash
KUBE_VERSION=1.21
K9S_VERSION=0.24.15

sudo snap install microk8s --classic --channel=${KUBE_VERSION}
microk8s status --wait-ready
microk8s kubectl get nodes
printf "alias kubectl='microk8s kubectl'\n" >> ~/.bash_aliases
printf "alias helm='microk8s helm3'\n" >> ~/.bash_aliases
source ~/.bash_aliases
microk8s enable dns storage dashboard fluentd helm3
microk8s enable metallb:192.168.1.240/24
microk8s enable traefik
microk8s config > ~/.kube/valyria.config
KUBECONFIG=~/.kube/valyria.config; export KUBECONFIG

curl -LO https://github.com/derailed/k9s/releases/download/v${K9S_VERSION}/k9s_Linux_x86_64.tar.gz
tar zxvf k9s_Linux_x86_64.tar.gz
sudo cp k9s /usr/local/bin/
```

## TODO

The purpose is to use automation to install and configure as much as possible. I also want to become less dependent on using microk8s as the k8s implementation.

- DONE: Increase RAM from 2GB to 8GB.
- DONE: Increase vCPU from 1 to 2 cores.
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
