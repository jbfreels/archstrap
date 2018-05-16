# archstrap
`mkfs.ext4 /dev/sdc1`

`mkswap /dev/sdc5`

`swapon /dev/sdc5`

`mkdir /mnt && mount /dev/sdc1 /mnt`

`pacstrap -i /mnt base base-devel linux-lts linux-lts-headers vim --ignore linux`

`genfstab -U /mnt >> /mnt/etc/fstab`

Edit locale.gen `vim /etc/locale.gen` and uncommment en_US.UTF-8

`ln -s /usr/share/zoneinfo/America/New_York /etc/localtime`

`echo LANG=en_US.UTF-8 > /etc/locale.conf && export LANG=en_US.UTF-8`

## Networking
`systemctl enable dhcpcd@eth0.service`

## Pacman
Edit `/etc/pacman.conf` and uncomment...

```
[multilib]
Include = /etc/pacman.d/mirrorlist
```
`pacman -Sy`

## User
Set root password

`passwd`

Create new user

`useradd -m -g users -G wheel,storage,power -s /bin/bash jbfreels && passwd jbfreels`

`pacman -S sudo`

`EDITOR=vim visudo`

## Grub
`pacman -S grub-bios`

`grub-install --target=i386-pc --recheck /dev/sdc`

`cp /usr/share/locale/en\@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo`

`grub-mkconfig -o /boot/grub/grub.cfg`

# First boot
`exit`

`umount /mnt && reboot`


