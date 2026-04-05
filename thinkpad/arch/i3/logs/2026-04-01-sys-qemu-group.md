## what
set up `libvirt` and user permissions for qemu/virt-manager

## why
required to run virtual machines without root and allow virt-manager to connect

## Commands

```bash
sudo systemctl enable --now libvirtd

sudo usermod -aG libvirt $(whoami)
sudo usermod -aG kvm $(whoami)

sudo virsh net-start default
sudo virsh net-autostart default
```

## Output

- libvirtd enabled and running
- user added to libvirt and kvm groups
- default network started and set to autostart
