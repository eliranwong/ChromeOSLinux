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

<b>CPU:</b>

> dpkg --print-architecture

amd64

<b>python3:</b> Python 3.7.3

# Basics

Make sure you have the latest version of Chrome OS first, because "sudo apt update" does not work in some old Chrome OS versions.

1) Open Settings > About Chrome OS > Check for updates

2) Restart after updates if any

3) Open Settings > Linux (Beta) > Turn On

4) To check the Linux's version installed, open terminal and type:<br>
> cat /etc/os-release<br>
If the version is not 10 (buster) or above, you'll need to run the update script:<br>
> sudo bash /opt/google/cros-containers/bin/upgrade_container

5) To update packages, run on terminal app:
> sudo apt update && sudo apt dist-upgrade

6) To enable ADB debugging: Settings > Linux > Develop Android apps > Enable ADB debugging

7) To use microphone with Linux app: Settings > Linux > Allow Linux to access your microphone. [Remarks: Microphone setting here cannot be changed if Linux container is running.  Make sure to shut down Linux container first before changing this option.] 

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

apt:

https://github.com/eliranwong/ChromeOSLinux/blob/main/package_mx/apt.md

dpkg:

https://github.com/eliranwong/ChromeOSLinux/blob/main/package_mx/dpkg.md

flatpak:

https://github.com/eliranwong/ChromeOSLinux/blob/main/package_mx/flatpak.md

To install synaptic:

> sudo apt install synaptic

To run synaptic without root privileges:

> synaptic-pkexec

Enable root privileges:

First give your linux container access to the host display.  Please note that chrome OS is the host.]<br>
> xhost +si:localuser:root

If you do not want to enter the line above each time you run synaptic:

> echo "xhost +si:localuser:root" >> ~/.profile

Then, you can run synaptic with sudo command:

> sudo synaptic

# Basic Tools & Libaries

To install some basic command line tools and libraries, run:

> sudo apt install apt-utils build-essential cmake tree wget curl git zip unzip xz-utils nano lib32stdc++6 sqlite3 libsqlite3-dev libasound2 libnss3 libncurses5 libncurses5-dev libgl1-mesa-dev mesa-utils lsb-release binutils youtube-dl ffmpeg gawk opencc mlocate gnome-keyring libssl-dev libffi-dev libstdc++5 -y

# Input Method - fcitx

e.g. Chinese pinyin

https://github.com/eliranwong/ChromeOSLinux/blob/main/input_method/fcitx.md

# Use fcitx in GUI Applications

Add the following variables to work with fcitx (You may read the previous section about fcitx setup.),

> sudo nano /etc/systemd/user/cros-garcon.service.d/cros-garcon-override.conf

Environment="QT_QPA_PLATFORM=wayland"<br>
Environment="GDK_BACKEND=x11"

> nano ~/.bashrc

export QT_QPA_PLATFORM=wayland<br>
export GDK_BACKEND=x11

[Remarks: Without these settings, fcitx may still work, but not selection panel of Chinese characters.]

References on wayland: <br>
https://chromium.googlesource.com/chromiumos/platform2/+/HEAD/vm_tools/sommelier/README.md<br>
https://wiki.archlinux.org/index.php/wayland

# A note on Chrome OS wayland

It is observed that changing accessiblity settings, like "Large mouse cursor", after Linux virtual machine is created can cause display issues with some gui applications.  Some gui applications keep close and reopen and make them unusable.  It is possible that there is a bug that comes with the built-in wayland compositor as the error message indicates, e.g.:

* qt.qpa.wayland: Ignoring unexpected wl_surface.enter received for output with id: 7 screen name: "Screen5" screen model: "202B" This is most likely a bug in the compositor.

# Add Fonts

To install additional fonts, e.g. ubuntu fonts:

1) Download the latest version of Ubuntu Fonts from http://font.ubuntu.com/ or run:<br>
> wget https://assets.ubuntu.com/v1/0cef8205-ubuntu-font-family-0.83.zip

2) Unzip font package:<br>
> unzip 0cef8205-ubuntu-font-family-0.83.zip

3) Create user fonts directory:<br>
> mkdir -p ~/.fonts

4) Copy ubuntu fonts to user fonts directory:<br>
> cp -r ubuntu-font-family-0.83/ ~/.fonts

5) Build fonts information cache files:
> fc-cache -f -v

# Text Editor

nano

> sudo apt install nano -y

Move down a page: "ctrl + v"

Move up a page: "ctrl + y"

Quick jump to the end of the file: "ctrl + _" & "shift + v"

Quick jump to the end of the file: "ctrl + _" & "shift + y"

# Terminal

The built-in "Terminal" app that comes with Chrome OS is nice, but terrible for typing non-English characters, like Chinese.  Chinese characters are misplaced as one type.  We need a terminal app that have the following features:

* good support of copy & paste feature
* support unicode
* works with fcitx (gnome-terminal, unfornately does not work with fcitx)
* customisable

"urxvt" not matches all the requirements listed above, but also enable some other gui applications to work with fcitx.  You may read our notes about this:

https://github.com/eliranwong/ChromeOSLinux/blob/main/terminal/rxvt-unicode.md

and

https://github.com/eliranwong/ChromeOSLinux/blob/main/input_method/fcitx.md

# Browser

Take firefox as an example.  There are several ways to install firefox.  Firefox website suggests Chrome OS users to use flatpak to install firefox.  However, the firefox installed through flatpak does not work with input method fcitx.

To work with fcitx, install firefox via either of the following methods:

<b>esr version:</b>

> sudo apt install -y firefox-esr

To launch the installed esr version:

> firefox-esr

<b>full version:</b>

Download firefox package (*.tar.bz2) at:

https://www.mozilla.org/firefox/linux/?utm_medium=referral&utm_source=support.mozilla.org

Run in terminal:

> sudo apt install -y libstdc++5

> cd ~

> tar xjf firefox-*.tar.bz2

> rm firefox-*.tar.bz2

To launch the installed firefox:

> ~/firefox/firefox

Set a shortcut:

> echo "alias firefox=$HOME/firefox/firefox" >> ~/.bashrc

# Office Apps

We prefer WPS office.  It has better compatability with Microsoft documents than libreoffice.

Download the Linux Deb package from https://www.wps.com/

Right click the downloaded deb package and select "Install with Linux (Beta)"

# Test Audio

Update to the latest Chrome OS to get audio support for Linux apps.

Test: Open a youtube video with Linux firefox.

Remarks: Audio is not supported in some old versions of Chrome OS.

# Audio Editor

> sudo apt install audacity

Enable to use microphone for recording:

1) Shutdown Linux container first [right-click Terminal app icon on the shelf & select "Shut down Linux (Beta)"]
2) Enable to use microphone with Linux app: Settings > Linux > Allow Linux to access your microphone.
3) Launch Terminal app and audacity

> audacity

4) Select "default: Mic:0" on microphone option

# Scaling Individual Applications

If you find the installed audacity too small on screen, you may want to scale it up.

> echo 'alias audacity="sommelier -X --scale=0.5 --dpi=120 audacity"' >> ~/.bashrc

Read more at: https://www.reddit.com/r/Crostini/wiki/howto/adjust-display-scaling#wiki_adjusting_display_scaling_per_application

# Development Tools

<b>Android Studio + Flutter + Dart + connecting flutter to chromebook</b>

We found the following way is the easiest one to setup Android Studio together with flutter and dart.  Overall, it is easier to first install Android Studio then flutter and dart.

https://github.com/eliranwong/ChromeOSLinux/blob/main/development/AndroidStudioFlutter.md

<b>VS Code:</b>

https://github.com/eliranwong/wsl2/blob/master/programming/vs_code.md

<b>python3:</b>

sudo apt install build-essential python3 python-setuptools python3-pip python3-dev python3-venv libssl-dev libffi-dev -y

<b>nvm:</b>

> wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash
> source .bashrc

<b>note:</b>

> nvm install node

# Bible Apps

Unique Bible App Desktop

https://github.com/eliranwong/ChromeOSLinux/blob/main/bible/UniqueBibleApp.md

Unique Bible App Hybrid

https://github.com/eliranwong/UniqueBibleAppHybrid

# Useful Command Line Tools

https://github.com/eliranwong/wsl2/tree/master/cli_tools
