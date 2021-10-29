# valyria-notes

## Misc tools

```bash
K8S_VERSION=1.22
K8S_CLI_VERSION=1.22.3
K8S_CLUSTER_NAME=valyria

K9S_VERSION=0.24.15

cd /tmp
curl -LO https://github.com/derailed/k9s/releases/download/v$K9S_VERSION/k9s_Linux_x86_64.tar.gz
tar zxvf k9s_Linux_x86_64.tar.gz
sudo cp k9s /usr/local/bin/

curl -o kubectl -L https://dl.k8s.io/release/v$K8S_CLI_VERSION/bin/linux/amd64/kubectl
chmod +x kubectl
sudo mv kubectl /usr/local/bin

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

```
