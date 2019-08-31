# Archlinux_install
learn to install archlinux and i3

1.dd bs=4M if=/path/to/archlinux.iso of=/dev/sdb status=progress && sync 
  #lsblk or fdisk -l to find the disk

2.timedatetcl set-ntp true

3.wifi-menu

4.update_mirrorlist
  nano /etc/pacman.d/mirrorlist
  use ctrl+k ctrl+u F6 to search
  

5.pacman -Syy

6./dev/sda1 /boot +500M
  /dev/sda2 /swap +8G
  /dev/sda3 /mnt
  /dev/sda4 /home
  
  mkfs.fat -F32 /dev/sda1
  mkfs.ext4 /dev/sda3
  mkfs.ext4 /dev/sda4
  mkswap /dev/sda2
  swapon /dev/sda2
  

7.mount /dev/sda3 /mnt
  mkdir -p /mnt/boot/efi
  mount /dev/sda1 /mnt/boot/efi
  mkdir /mnt/home
  mount /dev/sda4 /mnt/home
  

8.pacstrap /mnt base base-devel



9.genfstab -U -p /mnt > /mnt/etc/fstab

###################################################################################


10.arch-chroot /mnt


