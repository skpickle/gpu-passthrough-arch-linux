# gpu-passthrough-arch-linux

1) enable iommu going to /etc/default and editing the grub file using nano (sudo nano grub)
2) update grub using this command as root grub-mkconfig -o /boot/grub/grub.cfg 
3) check if its enabled with this command sudo dmesg | grep -i -e DMAR -e IOMMU it should read intel_iommu=on somewhere
4) isolate your gpu by adding the ids of the gpu to a new file to: /etc/modprobe.d/ and the file should contain this "options vfio-pci ids=10de:13c2,10de:0fbb"
5) then go to /etc/mkinitcpio.conf and add this to "modules=(... vfio_pci vfio vfio_iommu_type1 vfio_virqfd ...)" and this to the very last HOOKS entry "HOOKS=(... modconf ...)"
