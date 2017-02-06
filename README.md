# ArchMate

A collection of scripts for a fast an easy installation of all software, icons, themes, cursors, ... automatically.


I will be using the following elements : 


Sardi icons at AUR and [Sourceforge](https://sourceforge.net/projects/sardi/files/)

Surfn icons at AUR and [Github](https://github.com/erikdubois/Surfn)

Aureola conky at [Github](https://github.com/erikdubois/aureola)

Plank themes at [Github](https://github.com/erikdubois/plankthemes)

More info can be found on http://erikdubois.be


#Screenshots


![Screenshots](http://i.imgur.com/ObfyXcV.jpg)


#Tutorials


Installation of Arch Linux is documented on https://erikdubois.be


##1. Arch installation

Archlinux installation can be found in this article. It will be shown in VirtualBox in order to be able to make a tutorial. Remember to choose the proper graphical driver and not the virtual box driver when installing on a ssd or harddisk.

http://erikdubois.be/how-to-install-arch-linux/


##2. Desktop environment installation


This installation on Arch Linux can be found in this article

http://erikdubois.be/how-to-install-openbox-on-arch-linux/


#Remember

##Change from qwerty to azerty in openbox

setxkbmap -model pc101 -layout be


# Youtube sources

Arch Linux Openbox playlist

https://www.youtube.com/playlist?list=PLlloYVGq5pS58Uc7Dgnu-Fk1BsS5Nnk6p


Showing all sardi and surfn icons.

https://www.youtube.com/watch?v=EHjCRJ3FdG0





# F  A  Q
--------------------

#What can you do if the script does not execute?

Since I sometimes forget to make the script executable, I include here what you can do to solve that.

A script can only run when it is marked as an executable.

	ls -al 

Above code will reveal if a script has an "x". X meaning executable.
Google "chmod" and "execute" and you will find more info.

For now if this happens, you should apply this code in the terminal and add the file name.

	chmod +x typeyourfilename

Then you can execute it by typing

	./typeyourfilename

Or you can follow these steps

![Screenshots](http://i.imgur.com/vXsOaFL.gif)


-------------------------------------------------
#But that is the fun in Linux.

You can do whatever <b>Y O U</b> want.

Share the knowledge.

I share my knowledge at http://erikdubois.be
------------------------------------------------







# ArchMate

Installing notes for my personal use.


Sardi v 7.2.9 at [Sourceforge](https://sourceforge.net/projects/sardi/files/)

![Screenshots](http://i.imgur.com/ObfyXcV.jpg)



# FASE 1

Steps to take when installing Mate from scratch

Pop in the latest arch usb

loadkeys be-latin1

cfdisk /dev/sda

delete all partitions

sda1 	/ everything minus 8GB for swap making sure it is primary and bootable (asterisk!)

sda2 		/swap	8 GB primary type swap (82)	

write - yes -quit

mkfs.ext4 /dev/sda1

mkswap /dev/sda2

swapon /dev/sda2

mount /dev/sda1 /mnt

pacman -Sy


pacstrap -i /mnt base base-devel

genfstab -U /mnt >> /mnt/etc/fstab

arch-chroot /mnt /bin/bash

nano /etc/locale.gen

uncomment these lines

	be_BY.UTF8
	en_GB.UTF8
	en_US.UTF8

CTRL + X , yes, enter

locale-gen

echo LANG=en_US.UTF-8 > /etc/locale.conf


export LANG=en_US.UTF-8

nano /etc/vconsole.conf

	KEYMAP=be-latin1
	FONT=lat9w-16

CTRL + X , yes, enter

ln -s /usr/share/zoneinfo/Europe/Brussels /etc/localtime

hwclock --systohc --utc

echo ArchErik > /etc/hostname

nano /etc/hosts


	<ip-address> <hostname.domain.org> <hostname>
	127.0.0.1 localhost.localdomain localhost ArchErik
	::1   localhost.localdomain localhost ArchErik
	touch /etc/udev/rules.d/80-net-setup-link.rules

pacman -S networkmanager

systemctl enable NetworkManager

mkinitcpio -p linux

passwd

pacman -S grub os-prober

grub-install --target=i386-pc --recheck /dev/sda

grub-mkconfig -o /boot/grub/grub.cfg

umount /dev/sda1

exit

reboot







#FASE 2 root

login with root
and use the password

useradd -m -g users -G wheel,storage,power -s /bin/bash erik

passwd erik

EDITOR=nano visudo

Look for these lines with an hashtag in front
	
	 %wheel ALL=(ALL) ALL

hashtag (#) should be gone

CTRL = X , yes and enter


pacman -S bash-completion

if no internet - again

sudo systemctl enable NetworkManager

sudo systemctl start NetworkManager


exit







# FASE 3 Personal login and xserver


Login with new account i.e. here erik and password



sudo pacman -S xorg-server xorg-server-utils xorg-xinit xorg-twm xterm


sudo pacman -S xf86-video-nouveau





# FASE 4 Desktop environment


sudo pacman -S mate mate-extra





# FASE 5 Display manager

easy switching between desktop environments and login

sudo pacman -S gdm

systemctl enable gdm.service

systemctl start gdm.service


change your keyboard to belgian in the settings



# Fase 5 Getting our software

export EDITOR=nano


sudo pacman -S firefox

Surf to https://github.com/erikdubois/ArchMate

If you download the zip

	
sudo pacman -S file-roller

Download and right mouse click to extract

If you work with git

sudo pacman -S git

git clone https://github.com/erikdubois/ArchMate


Go inside the folder and run every program in there


./0 added this to start xserver, desktop environment and display manager


./1 and press tab etcetera


./2 ...


./3 ...


run forest run


# Tips


printscreen keyboard shortcut

scrot -e ~/Pictures/capt-$(date '+%Y-%m-%d-%H%M%S').png