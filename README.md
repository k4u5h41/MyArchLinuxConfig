# MyArchLinuxConfig

💻 -1nf1n17yk1ng-

## Arch Installation
Download ISO : https://archlinux.org/download/

Create a Bootable USB : https://www.balena.io/etcher/

### Connect to Wifi
```
iwctl
[iwd]# help
[iwd]# station wlan0 connect "ETID62561"
give the password and exit
[iwd]# exit
ping 8.8.8.8
```
### Create Partitions
```
mkfs.ext4 /dev/sda (format harddsisk)

If you needed to partition the drive manually, like you were setting up in a virtual machine, I would recommend using cfdisk.
cfdisk /dev/sda (select DOS)
(Nomarlly I give 10G Swap(/dev/sda1), 450GB root Partition (/dev/sda2))

mkfs.ext4 /dev/sda2
mkswap /dev/sda1
swapon /dev/sda1
```
### Mounting the Filesystem
```
mount /dev/sda2 /mnt
```
### Installing Arch
```
pacstrap /mnt base linux linux-firmware nano vim
```
### Configure the system
```
genfstab -U /mnt >> /mnt/etc/fstab
```
### Chroot into the new filesystem
```
arch-chroot /mnt
```
### Set the time zone
```
ln -sf /usr/share/zoneinfo/Europe/Zurich /etc/localtime
hwclock --systohc
```
### Localization
```
nano /etc/locale.gen (uncomment en_US.UTF-8 UTF-8)
locale-gen 
nano /etc/locale.conf (LANG=en_US.UTF-8)
```
### Create the hostname
```
nano /etc/hostname
nano /etc/hsots
```
![image](https://user-images.githubusercontent.com/66146701/130053018-bc10c6c0-8d62-4329-8413-0a46522a0c7f.png)

### Set the root password
```
passwd
```
### setup sudo user
```
pacman -S sudo
useradd -mG wheel username
EDITOR=nano visudo
passwd username
```
### Install NetworkManager
```
pacman -S networkmanager
systemctl enable NetworkManager
```
### Install Grub
```
pacman -S grub
grub-install --target=i386-pc /dev/sda
grub-mkconfig -o /boot/grub/grub.cfg
```

```
exit -a
reboot
```
## Mate Installation

```
nmtui (Connect to wifi)
ping 8.8.8.8
```
### Install Packages
```
sudo pacman -S xorg xorg-server os-prober base-devel linux-headers mata mate-extra lightdm libreoffice terminator firefox chromium mpv
```
### Install yay
```
sudo pacman -S git go
mkdir Tools
cd Tools
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
```
### Lightdm Config
```
yay -S lightdm-slick-greeter
nano /etc/lightdm/lightdm.conf (uncomment greeter-session and change greeter-session to lightdm-slick-greeter)
sudo systemctl enable lightdm
```
### Themes
```
yay -S arc-gtk-theme arc-icon-theme papirus-icon-theme
```
