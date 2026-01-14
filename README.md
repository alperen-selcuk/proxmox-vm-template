# proxmox-vm-template

first create normal VM and named ubuntu-template then delete attched disk. 

add cloudinit drive and provide username password. also ssh key if you want. 

ssh proxmox serveer where template machine was crated.

find exact server image for example i will use ubuntu2404

you can find from this link https://cloud-images.ubuntu.com/minimal

copy the img link https://cloud-images.ubuntu.com/minimal/releases/noble/release/ubuntu-24.04-minimal-cloudimg-amd64.img

type these command:

```
wget https://cloud-images.ubuntu.com/minimal/releases/noble/release/ubuntu-24.04-minimal-cloudimg-amd64.img
mv ubuntu-24.04-minimal-cloudimg-amd64.img ubuntu-2404.qcow2
qm set 10000 --serial0 socket --vga serial0
qemu-img resize ubuntu ubuntu-2404.qcow2 32G
qm importdisk 10000 ubuntu-2404.qcow2 local-lvm
```

so if we look VM hardware detail from proxmox dashboard 

you can find unused disk we attached in server.

edit with below configuration and add.
- discard -> OK
- SSD emulation -> OK
- IOthread -> NOK
