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

11.ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime


12.hwclock --systohc --utc


13.nano /etc/locale.gen

14.locale-gen

15.echo "LANG=en_US.UTF-8" > /etc/locale.conf

16.passwd 
   *set root passwd

7.echo $hostname > /etc/hostname

8.vi /etc/hosts
127.0.0.1    localhost
::1          localhost
127.0.1.1    hostname.localdomain    hostname

19. pacman  -S grub efibootmgr  iw wpa_supplicant dialog intel-ucode networkmanager network-manager-applet dhcpcd

20. mkinitcpio -p linux

20. grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=grub
    grub-mkconfig -o /boot/grub/grub.cfg
    

21.useradd -m -g users -G wheel -s /bin/bash username
   passwd username
   
22.pacman -S sudo

23.输入nano /etc/sudoers，进入界面后找到
   %wheel ALL=(ALL)ALL
   这一行并把#去掉，找到#%sudo ALL=(ALL) ALL把%sudo替换为你的用户名，最后同样去掉#保存退出

24.pacman -S gdm  evince  git unrar p7zip wget git ntfs-3g vim

25.pacman -S xf86-video-intel xf86-input-libinput

26.pacman -S ttf-dejavu wqy-microhei noto-fonts-emoji adobe-source-code-pro-fonts adobe-source-han-sans-cn-fonts

27.pacman -S xorg-server xorg-xinit xorg-apps mesa xterm

28.pacman -S xf86-video-intel lib32-intel-dri lib32-mesa lib32-libgl

29. systemctl enable lightdm

30.systemctl start NetworkManager
   
   systemctl enable NetworkManager


31.nano /etc/pacman.conf

   按F6输入multilib找到#[multilib]那一行，并把那一行和它下一行的Include的#去掉，然后找到#[custom]去掉里面的custom和前面的#并把custom替换为   archlinuxcn并把它下两行的#去掉找到server那一行把=后面的去掉替换为
    https://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/$arch
  然后找到 SigLevel = TrustedOnly这一行删去它，保存退出就可以了
       pacman -Syy archlinuxcn-keyring
       
32. sudo pacman -S yay 
    
33.    sudo pacman -S fcitx-gtk2 fcitx-gtk3 fcitx-qt4 fcitx-qt5 fcitx-configtool
   通过上面的命令安装好了还不够的，需要在/home/username(你的用户名)下建立一个文件
   文件名：.xprofile
  
  写入以下内容：
  export GTK_IM_MODULE=fcitx
  export QT_IM_MODULE=fcitx
  export XMODIFIERS="@im=fcitx"
  export LANG=zh_CN.UTF-8
  export LANGUAGE=zh_CN:en_US
  
other::

1.when keyring wrong
sudo pacman-key -u



 
