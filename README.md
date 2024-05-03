# metalfish

Development repository for building automation around redfish.

## Installation

1. Enable nested virtualization on a WSL2 instance . Make sure you have the following in the wsl config  "C:\Users\username\.wslconfig"

```
[wsl2]

nestedVirtualization=true
```

2. Install libvirtd and other necessary packages inside WSL2

```
sudo apt install virt-manager
```

3. Set the user and group as root for virtd inside "/etc/libvirt/qemu.conf" in WSL2

```
user = "root"
group = "root"
```

5. Everytime you restart your WSL2 instance, do these steps and you are good to go

chmod g+rw /dev/kvm

chgrp kvm /dev/kvm

service libvirtd restart

service virtlogd restart