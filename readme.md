# rpi-thin-client

Raspberry pi thin client

## Description

Instructions for setting up a thin client with raspberry pi

## Dependencies

Alpine os

Download latest alpine rpi image, here is an example link: [Alpine OS for rpi](https://dl-cdn.alpinelinux.org/alpine/v3.19/releases/aarch64/alpine-rpi-3.19.1-aarch64.img.gz).

You should instead use the lastest rpi os image from [Alpine Downloads](https://alpinelinux.org/downloads).

# Instructions

Write alpine image to sd and boot, assuming your sd is /dev/sda
dd if=./alpine-rpi-3.19.0-aarch64.img of=/dev/sda

Run the following commands to go though Alpine setup and install as sys on your sd, run 
```
setup-alpine
#reboot when done
```
Login as root and install required packages
```
apk update
apk add openbox
apk add nano
```

Enable community repo
```
nano /etc/apk/repositories 
#uncomment the community repo and save
apk update
```

Install xorg packages
```
apk add xorg-server
setup-xorg-base 
mkdir .config
cp -a /etc/xdg/openbox/ .config/
apk add xf86-video-fbdev
apk add font-terminus
apk add xterm
apk add remmina
echo 'remmina &' >> .xinitrc
echo 'exec openbox-session' >> .xinitrc
```

Enable 1080p on the rpi if would like
```
nano /boot/config.txt 
#add the following
add hdmi_group=1
add hdmi_mode=31
#save file

reboot
```

## Usage

Login as root and start xorg with remmina
```
startx
```
Right click to access the openbox menu, and launch xterm terminal if you need it
Remmina will be auto launched, or you can launch it form the menu

