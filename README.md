# Chrome OS Linux

This repository contains notes about Linux setup on Chrome OS.  These are written for setting up environment for developing bible apps.

We also wrote some note about WSL2 setup on Windows: https://github.com/eliranwong/wsl2

# Tested Device & Versions

Notes in this repository are tested with the following device and os versions:

<b>Device: Pixelbook Go</b>

<b>Chrome OS Version:</b> 87.0.4280.152 (Official Build) (64-bit)

<b>Linux version:</b> 

> cat /etc/os-release

PRETTY_NAME="Debian GNU/Linux 10 (buster)"<br>
NAME="Debian GNU/Linux"<br>
VERSION_ID="10"<br>
VERSION="10 (buster)"<br>
VERSION_CODENAME=buster<br>
ID=debian<br>
HOME_URL="https://www.debian.org/"<br>
SUPPORT_URL="https://www.debian.org/support"<br>
BUG_REPORT_URL="https://bugs.debian.org/"

<b>Virtual machine:</b>

Checked with Chrome browser:

> chrome://components

cros-termina - Version: 13495.0.0

<b>python3:</b> Python 3.7.3

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

6) To enable ADB debugging: Settings > Linux > Develop Android apps > Enable ADB debugging

7) To use microphone with Linux app: Settings > Linux > Allow Linux to access your microphone.

Reference: https://support.google.com/chromebook/answer/9145439?hl=en-GB

# How to restart Linux virtual machine?

1) Right-click "Terminal" app icon on the "shelf".
2) Shut down Linux (Beta)
3) Start the "Terminal" app again

# Where to adjust disk size of Linux container?

Settings > Linux > Disk size > Change

To check disk storage, run:

> df -h

# Package management


To manage packages:

To show help of "apt" command:

> apt help

To display policy:

> apt policy

To update package information, upgrade installed packages and install necessary dependencies:

> sudo apt update && sudo apt dist-upgrade

To install a package ("-y" below is optional.  It simply says "yes".):

> sudo apt -y install [package]

To upgrade a package:

> sudo apt upgrade [package]

To upgrade a package and install new dependencies if necessary:

> sudo apt dist-upgrade [package]

To overwrite an installed old version without upgrading:

> sudo apt install [package] --no-upgrade

To remove a package without removing configuration files:

> sudo apt remove [package]

To remove a package together with configuration files:

> sudo apt purge [package]

To remove old downloaded archive files:

> sudo apt autoclean

To list installed packages:

> sudo apt list --installed

To list upgradable packages:

> sudo apt list --upgradable

To show a package information:

> apt show [package]

TO show a package dependency:

> apt depends [package]

To search for a package, e.g.:

> apt search fcitx

OR

> apt-cache search fcitx

# Basic Tools

To install some basic command line tools, run:

> sudo apt install apt-utils build-essential cmake tree wget curl git zip unzip xz-utils nano lib32stdc++6 sqlite3 libsqlite3-dev libasound2 libnss3 libncurses5 libncurses5-dev libgl1-mesa-dev mesa-utils lsb-release binutils youtube-dl ffmpeg gawk opencc mlocate -y

To enable Flatpak:
1) Run on terminal:
> sudo apt install flatpak -y
> flatpak --user remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
2) Restart Linux virtual machine
3) Try to install an app with flatpak, e.g.:
> flatpak install firefox
4) Try to run an app with flatpak, e.g.:
> flatpak run org.mozilla.firefox

Remarks: To add environment variable with flatpak, e.g. flatpak run --env=QT_QPA_PLATFORM=wayland APP [ARGUMENT?]

# Test Audio

Update to the latest Chrome OS to get audio support for Linux apps.

Test: Open a youtube video with Linux firefox.

Remarks: Audio is not supported in some old versions of Chrome OS.

# Input Method

e.g. Chinese pinyin

https://github.com/eliranwong/wsl2/blob/master/input_method/backup/fcitx.md

# Text Editor

nano, geany

> sudo apt install nano geany -y

# Development Tools

<b>Android Studio + Flutter + Dart + connecting flutter to chromebook</b>

We found the following way is the easiest one to setup Android Studio together with flutter and dart.  Overall, it is easier to first install Android Studio then flutter and dart.

https://github.com/eliranwong/ChromeOSLinux/blob/main/development/AndroidStudioFlutter.md

# Office Apps

WPS Office

# Bible Apps

Unique Bible App Desktop

https://github.com/eliranwong/ChromeOSLinux/blob/main/bible/UniqueBibleApp.md

Unique Bible App Hybrid

https://github.com/eliranwong/UniqueBibleAppHybrid
