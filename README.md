Cloning the repo

```
cd ~
git clone https://github.com/Odilhao/ex294-rhce-lab.git
cd ex294-rhce-lab
```

## ENV PREP

1. Installing Libvirt

```
sudo yum install libvirt
sudo systemctl enable libvirtd --now
```

2. Creating the Network for this LAB

```
sudo virsh net-destroy ex294
sudo virsh net-undefine ex294
sudo virsh net-define --file libvirt/net-ex294.xml
sudo virsh net-start ex294
sudo virsh net-autostart ex294
```

3. Downloading the Centos 8 Image

```
sudo wget http://mirror.rackspace.com/CentOS/8.1.1911/isos/x86_64/CentOS-8.1.1911-x86_64-boot.iso -O /var/lib/libvirt/images/CentOS-8.1.1911-x86_64-boot.iso
``` 

4. Creating the Servers:

Bastion

`sudo bash vms/bastion.sh`

Node-1

`sudo bash vms/node-1.sh`

Node-2

`sudo bash vms/node-2.sh`

Node-3

`sudo bash vms/node-3.sh`

Wait from 15 to 30 minutes, depending on your network speeds.

### Acessing the Env

The servers are all created with the root password **ansible**.

`ssh root@192.168.244.10`

From the bastion you can check the DNS for all nodes:


```
host node-1.ex294.lab.local
host node-2.ex294.lab.local
host node-3.ex294.lab.local
```