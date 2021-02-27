# gpu-passthrough-arch-linux

1) enable iommu going to /etc/default and editing the grub file using nano (sudo nano grub) adding intel_iommu=on
2) update grub using this command as root grub-mkconfig -o /boot/grub/grub.cfg 
3) check if its enabled with this command sudo dmesg | grep -i -e DMAR -e IOMMU it should read intel_iommu=on somewhere
4) isolate your gpu by adding the ids of the gpu to a new file called vfio.conf to: /etc/modprobe.d/ and the file should contain this "options vfio-pci ids=10de:13c2,10de:0fbb"
5) then go to /etc/mkinitcpio.conf and add this to "modules=(... vfio_pci vfio vfio_iommu_type1 vfio_virqfd ...)" and this to the very last HOOKS entry "HOOKS=(... modconf ...)"
6) now check on terminal the kernels in use by the gpu using lspci -vk and it should read "kernel driver in use vfio-pci"  
7) now lets install all the packages needed using sudo pacman -S qemu libvirt edk2-ovmf virt-manager ebtables dnsmasq 
8) add user to libvirt group sudo usermod -a -G libvirt "username" and newgrp libvirt 
9) verify with id username
10) enable and start libvirtd.service and its logging component virtlogd.socket using systemctl enable "service/socket" and systemctl start "service/socket"
11) enable default libvirt network using the following commands as root # virsh net-autostart default # virsh net-start default
