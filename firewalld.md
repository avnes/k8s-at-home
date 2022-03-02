# firewalld notes

## CheatSheet firewalld

```bash
firewall-cmd --list-all-zones # List all firewall zones
firewall-cmd --permanent --zone=libvirt --set-target=ACCEPT # Accept all incoming requests to servers in the libvirt zone
firewall-cmd --list-all --zone=libvirt # Show all settings for the libvirt zone
firewall-cmd --add-port=9000/tcp # Allow incoming requests on a port on the firewalld server
```
