# Chrome OS Linux

This repository contains notes about Linux setup on Chrome OS.  These are written for setting up environment for developing bible apps.

We also wrote some note about WSL2 setup on Windows: https://github.com/eliranwong/wsl2

# Tested Device & Versions

Notes in this repository works are tested with the following device and os versions:

- Device Pixelbook Go

- Chrome OS Version: 87.0.4280.152 (Official Build) (64-bit)

- Linux version: 

> cat /etc/os-release

PRETTY_NAME="Debian GNU/Linux 10 (buster)"
NAME="Debian GNU/Linux"
VERSION_ID="10"
VERSION="10 (buster)"
VERSION_CODENAME=buster
ID=debian
HOME_URL="https://www.debian.org/"
SUPPORT_URL="https://www.debian.org/support"
BUG_REPORT_URL="https://bugs.debian.org/"

- Virtual machine:

Checked with Chrome browser:

> chrome://components

cros-termina - Version: 13495.0.0

# Basics
Go to settings to get the latest version of Chrome OS first, "sudo apt update" does not work in some Chrome OS versions.

1) Open Settings > About Chrome OS > Check for updates

2) Restart after updates if any

3) Open Settings > Linux (Beta) > Turn On

4) To check the Linux's version installed, open terminal and type:
> cat /etc/os-release
If the version is not 10 (buster) or above, you'll need to run the update script:
> sudo bash /opt/google/cros-containers/bin/upgrade_container

5) To update packages, run on terminal app:
> sudo apt update && sudo apt dist-upgrade

Reference: https://support.google.com/chromebook/answer/9145439?hl=en-GB

# How to restart Linux virtual machine?

1) Right-click "Terminal" app icon on the "shelf".
2) Shut down Linux (Beta)
3) Start the "Terminal" app again

# Basic Tools

To enable Flatpak:
1) Run on terminal:
> sudo apt install flatpak -y
> flatpak --user remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
2) Restart Linux virtual machine
3) Try to install an app with Flatpak, e.g.:
> flatpak install firefox

