# virsh notes

## CheatSheet virsh

```bash
sudo virsh list --all       # List all domains
sudo virsh shutdown dragonlord  # Stop one domain
sudo virsh edit dragonlord  # Open an editor and tweak the VM settings
sudo virsh start dragonlord # Start one domain
virsh net-dhcp-leases default # get all VMs IP addresses
virsh net-dhcp-leases default | awk '{ print $5" " $6}' | sed "s/\/24//g" # Get nice output to put in /etc/hosts
```
