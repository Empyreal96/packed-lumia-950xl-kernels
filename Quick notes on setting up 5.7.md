# Quick notes on setting up..

This is just the process I did..



- Install firmware-atheros bluetooth bluemon bluez* rfkill rfcomm dhcpd
- Update Kernel to 5.7 using dpkg it will generate new initramfs (Don't reboot yet)

- Blacklist ath10k_pci module 

- copy rampatch_00440302.bin and nvm_00440302.bin to /lib/firmware/qca/ (the required files may be different if you have a different variant 950XL, check dmesg for what firmware fails to load)

- Add entry to grub.cfg (Example of mine):

  `set timeout=07

  menuentry "Debian Kernel 4.18.6" {
  	set background_color=black
  	insmod part_msdos
  	insmod ext2

  	set root=(hd0,gpt41)
  	linux /boot/vmlinuz-4.18.6-lumia-950xl-uefi root=UUID="969daa87-f176-4283-9d80-bbd899a687a8" video=efifb acpi=no rw
  	initrd /boot/initrd.img-4.18.6-lumia-950xl-uefi
  	
  	devicetree /boot/msm8994-microsoft-lumia-950xl.dtb

  }
  menuentry "Debian Kernel 5.7" {
  	set background_color=black
  	insmod part_msdos
  	insmod ext2

  	set root=(hd0,gpt41)
  	linux /boot/vmlinuz-5.7.0-lumia-950xl-uefi root=UUID="969daa87-f176-4283-9d80-bbd899a687a8" video=efifb acpi=no rw
  	initrd /boot/initrd.img-5.7.0-lumia-950xl-uefi
  	
  	devicetree /boot/msm8994-microsoft-lumia-950xl.dtb

  }`



- Reboot
- Make sure modules and firmware are loaded (btusb bnap ath10k_core and the .bin files with dmesg)
- Done, you should now be able to connect to Bluetooth networks (Pan/Dun etc)