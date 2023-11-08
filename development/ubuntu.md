# Install Ubuntu on Pixelbook Go

## Prepare a USB for Ubuntu Installation

Read https://ubuntu.com/tutorials/install-ubuntu-desktop#3-create-a-bootable-usb-stick

## Enable Developer Mode

1. back up data first
2. Press "Esc+Refresh+Power"
3. Ctrl+D
4. Enter
5. Ctrl+D

## Enabling Debugging Features

1. Select "Enable Debugging Features in set up screen
2. Enter root password

## Log in Deveoper Console

1. Press "Ctrl+Alt+T" to launch terminal
2. Run:
> shell
3. Press "Ctrl+Alt+F2/Refresh"
4. Enter login:
> root
5. Enter password that was set in enabling debugging features

## Enable Booting from USB

> enable_dev_usb_boot

> sudo crossystem dev_boot_usb=1

> sudo crossystem dev_boot_altfw=1

## Install Alternative Bootloader

> cd; curl -LO mrchromebox.tech/firmware-util.sh && sudo bash firmware-util.sh

Select "1"

## Reboot

1. Insert Ubuntu installation USB and reboot
2. At startup white screen, press "Ctrl+L"
3. Press "1"
4. Follow instructions about Ubuntu Installation
5. Remove Ubuntu installation USB and reboot

## Start Ubuntu

1. Press "Ctrl+L" at white screen
2. Press "1"

## Try to Fix Ubuntu Audio

> git clone https://github.com/WeirdTreeThing/chromebook-linux-audio

> cd chromebook-linux-audio

> ./setup-audio

# References

https://www.wikihow.com/Enable-USB-Booting-on-Chromebook

https://chromium.googlesource.com/chromiumos/docs/+/master/developer_mode.md#Booting-from-USB-or-SD-card

https://chromium.googlesource.com/chromiumos/docs/+/master/developer_mode.md#:~:text=By%20default%2C%20you%20can%20login,you%20can%20set%20a%20password

https://logmeonce.com/resources/2023/07/26/enable-debugging-features-chromebook-root-password/

https://mrchromebox.tech/#chromeos

https://askubuntu.com/questions/1468964/how-to-install-ubuntu-on-an-intel-amd-chromebook-google-pixelbook-2017

