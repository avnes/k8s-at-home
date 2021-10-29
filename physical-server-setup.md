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

## libvirt configuration

```bash
# Check if storage pool called 'default' exist, is started, and has autostart on
sudo virsh pool-list --all

# Create a storage pool called 'default' if missing
sudo virsh pool-define-as default dir - - - - "/var/lib/libvirt/images"
sudo virsh pool-build default
sudo virsh pool-start default
sudo virsh pool-autostart default
sudo virsh pool-list --all
sudo virsh pool-info default
```

## Resize logical volumes

I needed to resize my /home and / paritions too.  With XFS, shrink is not possible, so I had to delete /home first before creating it again:

```bash
umount /home
lvremove /dev/mapper/cs-home
lvcreate -n home -L 50G cs
mkfs.xfs /dev/cs/home
mount /dev/mapper/cs-home
```

I also need to recreate my home directory:

```bash
mkdir -p /home/audun
chown audun:audun /home/audun
```

Extend root partition:

```bash
# Find free space:
vgs cs
lvextend -L +230G /dev/cs/root -r
```

Create a data partition:

```bash
# Find free space:
vgs cs
lvcreate -n data -L 100G cs
mkfs.xfs /dev/cs/data
mkdir /data
mount /dev/mapper/cs-data /data
```

Add new data partition to automount:

```bash
echo "/dev/mapper/cs-data     /data                   xfs     defaults        0 0" >> /etc/fstab
```

## Automatic software patching

```bash
sudo dnf install -y dnf-automatic
sudo sed -i 's/^apply_updates.*/apply_updates = yes/g' /etc/dnf/automatic.conf
sudo sed -i 's/^upgrade_type.*/upgrade_type = security/g' /etc/dnf/automatic.conf
sudo systemctl enable --now dnf-automatic.timer
```
