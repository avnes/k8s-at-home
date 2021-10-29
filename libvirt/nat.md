# Port forwarding through NAT

## Configure firewall rules for libvirt

```bash
sudo mkdir -p /etc/libvirt/hooks/
sudo cp ./qemu /etc/libvirt/hooks/qemu
sudo chmod +x /etc/libvirt/hooks/qemu
sudo systemctl restart libvirtd.service

sudo virsh shutdown dragonlord
sudo virsh list --all # Wait for dragonlord to be down
sudo virsh start dragonlord

sudo virsh shutdown aegon
sudo virsh list --all # Wait for aegon to be down
sudo virsh start aegon

sudo virsh shutdown rhaenys
sudo virsh list --all # Wait for rhaenys to be down
sudo virsh start rhaenys

sudo virsh shutdown visenya
sudo virsh list --all # Wait for visenya to be down
sudo virsh start visenya
```

## Test firewall rules

```bash
ssh ansible@braavos -p 21022 -i ~/.ssh/valyria.pem # dragonlord
ssh ansible@braavos -p 21122 -i ~/.ssh/valyria.pem # aegon
ssh ansible@braavos -p 21222 -i ~/.ssh/valyria.pem # rhaenys
ssh ansible@braavos -p 21322 -i ~/.ssh/valyria.pem # visenya
```
