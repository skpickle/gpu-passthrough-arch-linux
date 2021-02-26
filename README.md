# gpu-passthrough-arch-linux

1) enable iommu going to /etc/default and editing the grub file using nano (sudo nano grub)
2) update grub using this command as root grub-mkconfig -o /boot/grub/grub.cfg 
3) check if its enabled with this command sudo dmesg | grep -i -e DMAR -e IOMMU
