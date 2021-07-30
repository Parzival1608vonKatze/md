# Arch Install 
* a Little guide to installing Arch Linux.
This is a very simple guide! If you run into any problems: keep calm, don't just try to go a head *if you do you may waste your time!* and as always the web is your best friend when someting goes wrong!
* [Arch-Wiki](https://wiki.archlinux.org)
* WARNING: This guide is not fully completed. And I am using some applications based on personal preference. Only replace those Apps during the install if you know what you're doing! After the install you can pretty much change out what you want! And my first language is german, so you may encounter typos/miss-spelling of some words!

                                                                           ██
                                                                          ████
                                                                         ██████
                                                                        ████████
                                                                       ██████████
                                                                      ████████████
                                                                     ██████████████
                                                                    ████████████████
                                                                   ██████████████████  
                                                                  ████████████████████
                                                                 ██████████████████████
                                                                ██████████     █████████
                                                               ██████████       █████████
                                                              ██████████         █████████
                                                             ███████████         ██████████
                                                            ████████████         ███████████
                                                           ████████                  ████████
                                                          ████                            ████
                                                         ██                                  ██
 
 ## 1.Pre-Install 
* if you ar intalling on bare metal try to use a ethernet-cable *normaly helps with network issues*
* ISO downloads [here](https://archlinux.org/download)
 ## 2.Install
### boot
* select 'Boot Arch Linux (x86_64)' in grub (bootloader)

### Keymaps
* if you use any other Keyboard layout than en-US read this (if use en-US or are fine with that skip to 'network')
* run: 'ls /usr/kbd/share/kbd/keymaps/**/*.map.gz'
* then: 'loadkeys {keymap}' (example:'loadkeys de-latin1')

### timedatectl  
* activating the time-date service
* run: 'timedatectl set-npt true'
* to check if the service is running run: 'timedatectl status'
### network
* if you need to use WIFI  run: 
'wifi-menu' *a menu to connect your PC/Laptop to your router/the Internet wirelessly*  
* to make sure that your internet connection is working:
'ping gnu.org' *or your Website of choice*
* press 'CTRL+C' after 30 seconds if it lost ANY packets search for help in the web (Forums!)
* 'clear' *to clear the screen*
### time
* to sync our clocks run 'timedatectl set-ntp true'
* then 'timedatectl status' *to check if the service is running*
### partitioning with cfdisk
* now we want to partition the drive 
* run 'lsblk' *to see all drives/drive lables/drive names!* anything starting with 'loop' or 'sr' is NOT your drive! The label of your drive will probably start with 'sd' or 'nvme' (or if the PC you're installing to is really old: 'ide')*depending on your drive type or connector*.
* know write down the name/label of the drive your want to install to!
* make sure that it's the right drive because we will later erase ALL of it's contents!
* then run: 'cfdisk'
* if you are installing to a drive thats larger than 2TB and are on a newer (UEFI) system choose 'gpt' otherwise choose 'dos'
#### boot partiiton we are going to create a boot partition!
* on A BIOS system
* now press enter on the *new* button (btw. you can navigate using the arrow keys!)
* enter '128M'; then 'primary'
* then (in the table) navitgate to the partition we created (probably named '/dev/sda1' or '/dev/nvme1') and hit 'b' to give it the boot flag (a '*' will be written under the boot section!)
#### main partition!
* now navigate back down to 'Free space' and hit enter on 'new' again !
* then give it the rest of the disk space and choose 'primary' !
* then navigate to 'write' and hit enter on it ! Then it's gonna prompt you if you really want to write to the disk you have to type 'yes' and hit enter!
* then navigate to 'quit' and hit enter on that!

### formating all partitions 
* run: 'mkfs.ext4 {label of the drive}{partition number}'
* do this for both partitions
* for example 'mkfs.ext4 /dev/sda1' and 'mkfs.ext4 /dev/sda2'
or 'mkfs.ext4 /dev/nvme1' and 'mkfs.ext4 /dev/nvme2' and so on...

### mounting partitions
* run 'mount {drivelabel}2 /mnt
* run  'mkdir /mnt/boot'
* run 'mount {drivelabel}1 /mnt/boot'

### pacstrap
* know you've allready done the most difficult part of the install!
* pacstarp is basicly installing the base Arch system for you
* run: 'pacstrap /mnt base base-devel linux linux-firmware nano vim'
* this could take a couple of minutes!

### fstab
* the fstab basicly contains all the drives that Linux might need when you're booting up
* run: 'genfstab /mnt'
* then run 'genfstab -U /mnt >> /mnt/etc/fstab'

### chroot
* run: 'arch-chroot /mnt /bin/bin'
* now we're finialy in the new Arch install. NOT on the USB or DVD anymore!
* run: 'pwd' if it outputs '/' everyting worked perfect!

### installing the networkmanager and grub2 (+ bash-completion)
* now we're installing the networkmanager so we have proper  access to the internet and we're installing our boot-loader 'grub' so our system can boot!
* run 'pacman -S networkmanager grub bash-completion dosfstools osprober mtools'
* then it's going to prompt you if you want to install these packages: type 'y' and hit enter
* now we will tell systemd to start the networkmanager at boot
* run: 'systemctl enable NetworkManager'
* then we want to install grub to the disk
* so run: 'grub-install {drivelabel}' (for example in my last install it was 'grub-install /dev/sdb')
* then: 'grub-mkconfig -o /boot/grub/grub.cfg'
* *if it didn't find 'linux image' and 'initrd image' you probaly forgot you probably forgot to pacstarp your Linux-Kernel  (so go back and do that otherwise you'll have a problem!)*

* ### User(s)
* setting a password for the root-user
* run: 'passwd' and type in the password you wan to use, hit enter (and then retype it)!
* adding your User:
* run: 'useradd -m {username;no capital letters or spaces!} (example: 'useradd -m parzival')
* to create a password for the user run: passwd {username} (then type and retype your password!)
* adding that user to some groups:
* run: 'usermod -aG wheel,audio,video,optical,storage {username} '
* just to be sure try to install 'sudo' run: 'pacman -S sudo'
* to edit sudoers file run: 'EDITOR=nano visudo' (or vim!) 
* find the line starting with %wheel and uncomment it (uncomment means you need to remove the '#' at the start of the line!)
* then save the file (in nano: 'CRTL+S, CRTL+X' | in vim: ':wq')

### selecting locale/language
* selecting locale/language
* run: 'nano /etc/locale.gen' (or 'vim /etc/locale.gen')
* now arrow down, find your language and uncomment it  (uncomment means you need to remove the '#' at the start of the line!)
* then save the file (in nano: 'CRTL+S, CRTL+X' | in vim: ':wq')
* after that run: 'locale gen'
* then: 'nano /etc/locale.conf' (this is a new file, so it's empty!)
* type: 'LANG={your locale}.UTF-8' (for example: 'LANG=en-US.UTF-8')
* then save the file like you did before (in nano: 'CRTL+S, CRTL+X' | in vim: ':wq')

### hostname
* setting the hostname for your computer
* run: 'nano /etc/hostname' (or vim)
* and type in the name you want to give your PC (don't use spaces and capital letters!)
* then save the file like you did before (in nano: 'CRTL+S, CRTL+X' | in vim: ':wq')
* making a hosts file:
* run: 'nano /etc/hosts'(or use vim!)
* there should aleady be 2 lines:
* '# Static tablelookup for hostnames.' and
* '# See hosts(5) for details.'
* add the following lines:
* '127.0.0.1  localhost'
* '::1        localhost'
* '127.0.1.1  {the hostname we just created}'
* then save the file like you did before (in nano: 'CRTL+S, CRTL+X' | in vim: ':wq')

### timezone
* setting the timezone
* run: 'ln -sf /usr/share/zoneinfo/{America, Europe,... *use TAB*}/{City} /etc/localtime' (for me this would be: 'n -sf /usr/share/zoneinfo/Europe/Berlin /etc/localtime' }
* run: 'exit'
* then: 'umount -R /mnt'
* run: 'reboot'


 ## 3.After Install 
* theoreticaly you have installed Arch-Linux. But you don't a graphical env.!
* now your have to choose your boot option in grub. Normaly the first is what you want to boot from (so just hit enter on 'Arch Linux')
* login with root (so just type 'root' and enter the password you set earlier in '### setting a password for the root-user')

### for sh**s and gigles
* run: 'pacman -S neofetch' if it prompts you hit 'y'
* now take a picture of your screen and send it to (me and) your friends!

### Xorg
* installing xorg:
* run: 'pacman -S xorg xorg-server' *this could take a while*
## Desktop env.
* we ar going to install gnome since it's the most popular desktop-env. and most people don't want to bother with window managers. Also in already includes a display-manager (gdm)! It's not difficult to install a Desktop env. just look it up! 
* run: 'pacman -S gnome gnome-extras' (we are also installing gnome extras since it includes a browser, media-player,..; you could just install FireFox/Chormium/Brave/...,Alactitty/Termite/Gnome-Terminal/..,gVim/gedit/leafpad/kate/...,mpv/vlc/... instead of gnome-extras; just make sure you install a terminal emulator otherwise you f***ed up!)
* it will probaly ask you a few times whitch packages you want to install, just stick with the defaults (1)
* starting the Display-Manager:
* run: 'systemctl enable gdm.service'
* reboot *the displaymanager is now gonna start at boot, but it will probally take a few seconds (at least on the first time*)

NOW YOU HAVE A USABLE Arch SYSTEM!

NOW YOU (ALREADY) COULD TELL ALL YOUR FRIENDS: 
                                                                  I USE ARCH BTW!

IF YOU'D RAHER WATCH A VIDEO:
* Arch Linux installation guide by DistroTube *on LBRY and Youtube*
* Arch Linux Installation Guide (Best on YouTube!) by Mental Outlaw *on LBRY and Youtube*
                                                                   (END OF FILE) 