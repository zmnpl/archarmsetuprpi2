# Arch ARM Setup

This is my variation of an Arch Linux Arm installation on a Raspberry PI 2. Mostly for my reference but should help others as well. I'm using the RPI for automation tasks like backups and as a server i.e. for Postgres for development and testing.

## Make SD card

Making the SD card is as simple as following the instructions on the download page. No further details needed.

## Boot

## Load German keyboard
    loadkeys de-latin1-nodeadkeys

## Switch to root
   su

## Add user
    useradd -m -g users -s /bin/bash simon
    passwd simon

## Sudo
    pacman -S sudo
    EDITOR=nano visudo

Uncommment this line
    #%wheel ALL=(ALL) ALL

Add user to group wheel
    gpasswd -a simon wheel

## Switch root password
    su
    passwd

## Delete standard user "alarm"
    userdel alarm

## Local settings

### /etc/locale.conf
    vim /etc/locale.conf
    echo LANG=de_DE.UTF-8
    LC_COLLATE=C
    LANGUAGE=de_DE

### /etc/localtime
ln -s /usr/share/zoneinfo/Europe/Berlin /etc/localtime

### /etc/locale.gen
Uncomment

    #de_DE.UTF-8 UTF-8
    #de_DE ISO-8859-1
    #de_DE@euro ISO-8859-15

### Generate locale
    locale-gen

## Enable SSH
    systemctl enable sshd.service
    systemctl start sshd.service

## ToDo - SSH Key for login without pw

## Pacman

### switch color on
    vim /etc/pacman.conf
    #Uncomment next line
    #Color

### update
    pacman -Syu

## Vim
    pacman -S vim

## Git
    pacman -S git

## Autofs
    pacman -S autofs

## Cron
    pacman -S cronie
    systemctl enable cronie

## Ntp
    pacman -S ntp
    systemctl enable ntpd.service
    systemctl start ntpd.service
    ntpd -gq
    hwclocl -w

## Zsh
    pacman -S zsh
    chsh
    /usr/bin/zsh

## Clone and install dotfiles

## Install further packages
    pacman -S screenfetch rsync getmail

## Enable USB to power external HDD

Add line to bottom of */boot/config.txt*
    max_usb_current=1

## ToDo wiring pi and a project on this