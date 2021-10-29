# Physical server setup

After installation of CentOS Stream on your hardware, you need to perform these tasks in order to have a solid base for running virtual machines etc.

## Packages and services

```bash
sudo dnf install -y python39 sysstat git libvirt cockpit cockpit-machines virt-manager
sudo systemctl enable cockpit.socket --now
sudo systemctl enable libvirtd --now
sudo firewall-cmd --zone=public --add-service=cockpit --permanent
sudo firewall-cmd --reload

sudo dnf config-manager --add-repo https://rpm.releases.hashicorp.com/RHEL/hashicorp.repo
sudo dnf install -y terraform
sudo usermod -a -G libvirt $(whoami)
```
