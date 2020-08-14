## ENV PREP

1. Installing Libvirt

```
sudo yum install libvirt
sudo systemctl enable libvirtd --now
```

2. Creating the Network for this LAB

```
cat <<EOF > /tmp/net-ex294.xml
<network>
  <name>ex294</name>
  <uuid>985236f4-75bf-89f7-f3f7-4c48f1f3a24c</uuid>
  <forward mode='nat'>
    <nat>
      <port start='1024' end='65535'/>
    </nat>
  </forward>
  <bridge name='virbr294' stp='on' delay='0'/>
  <mac address='02:78:13:be:43:22'/>
  <domain name='ex294.lab.local' localOnly='yes'/>
<dns>
    <host ip='192.168.244.10'>
      <hostname>bastion</hostname>
    </host>
    <host ip='192.168.244.21'>
          <hostname>node-1</hostname>
    </host>
    <host ip='192.168.244.22'>
          <hostname>node-3</hostname>
    </host>
    <host ip='192.168.244.23'>
          <hostname>node-3</hostname>
    </host>
  </dns>
  <ip address='192.168.244.1' netmask='255.255.255.0'>
    <dhcp>
      <range start='192.168.244.100' end='192.168.244.240'/>
    </dhcp>
  </ip>  
</network>
EOF

sudo virsh net-destroy ex294
sudo virsh net-undefine ex294
sudo virsh net-define --file /tmp/net-ex294.xml
sudo virsh net-start ex294
sudo virsh net-autostart ex294
```

3. Downloading the Centos 8 Image

```
sudo wget http://mirror.rackspace.com/CentOS/8.1.1911/isos/x86_64/CentOS-8.1.1911-x86_64-boot.iso -O /var/lib/libvirt/images/CentOS-8.1.1911-x86_64-boot.iso
``` 