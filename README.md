# Chrome OS Linux

This repository contains notes about Linux setup on Chrome OS.  These are written for setting up environment for developing bible apps.

We also wrote some note about WSL2 setup on Windows: https://github.com/eliranwong/wsl2

# Tested Device & Versions

Notes in this repository are tested with the following device and os versions:

<b>Device 1: Google Pixelbook Go</b>

<b>Chrome OS Version:</b> 107.0.5304.110 (Official Build) (64-bit)

<b>Device 2: Apple mac mini (2012)</b>

<b>Chrome OS Flex Version:</b> 108.0.5359.111 (Official Build) (64-bit)

<b>Linux version:</b> 

> cat /etc/os-release

PRETTY_NAME="Debian GNU/Linux 11 (bullseye)"<br>
NAME="Debian GNU/Linux"<br>
VERSION_ID="11"<br>
VERSION="11 (bullseye)"<br>
VERSION_CODENAME=bullseye<br>
ID=debian<br>
HOME_URL="https://www.debian.org/"<br>
SUPPORT_URL="https://www.debian.org/support"<br>
BUG_REPORT_URL="https://bugs.debian.org/"

<b>CPU:</b>

> dpkg --print-architecture

amd64

# System Info Viewer

Cog is a nice extension to view system information:

https://chrome.google.com/webstore/detail/cog-system-info-viewer/difcjdggkffcfgcfconafogflmmaadco?hl=en

# Check the zRam enabled by default

Press "ctrl + alt + t" key combination to open a crosh session and run:

> free -ht

Can use "swap" command to allocate the size of virtual memory instead of the default one, but it is unnecessary in common cases.

To change virtual memory, e.g.:

> swap enable 2048

To change to factory default:

(If the size is omitted, the factory default is chosen)

> swap enable

Remarks: Restart device for change in virtual memory to take effect.

Read https://support.google.com/chromebook/thread/93286060/want-to-increase-virtual-ram-memory-in-chromebook?hl=en

# Turn ON Linux

Make sure you have the latest version of Chrome OS first, because "sudo apt update" does not work in some old Chrome OS versions.

1) Open Settings > About Chrome OS > Check for updates

2) Restart after updates if any

3) Open Settings > Linux > Turn On

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
2) Shut down Linux
3) Start the "Terminal" app again

# Where to adjust disk size of Linux container?

Settings > Linux > Disk size > Change

To check disk storage, run:

> df -h

# Share Chrome OS Folder(s) with Linux

To access chrome os files from Linux side.

e.g.  Open "Files" app, right-click "Downloads" and select "Share with Linux"

# Package management

apt:

https://github.com/eliranwong/ChromeOSLinux/blob/main/package_mx/apt.md

dpkg:

https://github.com/eliranwong/ChromeOSLinux/blob/main/package_mx/dpkg.md

flatpak [avoid flatpak if possible if you want your downloaded apps to work with fcitx]:

https://github.com/eliranwong/ChromeOSLinux/blob/main/package_mx/flatpak.md

synaptic:

https://github.com/eliranwong/ChromeOSLinux/blob/main/package_mx/synaptic.md

# Basic Tools & Libaries

To install some basic command line tools and libraries, run:

> sudo apt -y install software-properties-common dirmngr apt-transport-https lsb-release ca-certificates apt-utils build-essential cmake tree wget curl git zip unzip xz-utils nano micro w3m lynx lib32stdc++6 sqlite3 libsqlite3-dev libasound2 libnss3 libncurses5 libncurses5-dev libgl1-mesa-dev mesa-utils libglu1-mesa lsb-release binutils ffmpeg gawk opencc plocate gnome-keyring libssl-dev libffi-dev libstdc++5 libpci3 libpci-dev python3 python-setuptools python3-pip python3-dev python3-venv zlib1g-dev libgdbm-dev libnss3-dev libreadline-dev libbz2-dev gcc xorg-dev exo-utils dex

# Input Method - fcitx

e.g. Chinese pinyin

https://github.com/eliranwong/ChromeOSLinux/blob/main/input_method/fcitx.md

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

Remarks: font directory lists are placed in /etc/fonts/fonts.conf

# Add Fonts with font-viewer

> sudo apt install -y font-viewer font-manager-common

For example:

1. download Hebrew fonts from https://www.1001fonts.com/hebrew-fonts.html
2. unzip the downloaded zip files
3. double click a font file in pcmanfm to launch '/usr/libexec/font-manager/font-viewer'
4. press 'install font'

# Text Editor

nano

> sudo apt install nano -y

Move down a page: "ctrl + v"

Move up a page: "ctrl + y"

Quick jump to the end of the file: "alt + \\"

Quick jump to the end of the file: "alt + /"

# Terminal

The built-in "Terminal" app that comes with Chrome OS is generally nice.  However, it is not good for typing non-English characters, like Chinese.  Chinese characters are misplaced as one type.  We want a terminal app that:

* supports copy & paste operations
* supports unicode
* works with fcitx
* allow customisation

We tested different terminal app on Chrome OS.  The best options we found are 'konsole' and 'rxvt-unicode'.

To install 'konsole', run:

> sudo apt install -y konsole

To copy, press 'ctrl+shift+c'

To paste, press 'ctrl+shift+v'

To run 'konsole' as login shell by default:

Settings > Configure Konsole > Profiles > Profile 1 (Default) > Edit > General > Command > /bin/bash -l

To change 'konsole' font, e.g. to Noto Sans Mono:

Settings > Configure Konsole > Profiles > Profile 1 (Default) > Edit > Appearance > Font > Noto Sans Mono

To support fcitx when konsole is launched via desktop file:

> sudo nano /usr/share/applications/org.kde.konsole.desktop

Change from:

> Exec=konsole

to:

> Exec=env QT_IM_MODULE=fcitx5 /usr/bin/konsole

For 'rxvt-unicode', read:

https://github.com/eliranwong/ChromeOSLinux/blob/main/terminal/rxvt-unicode.md

Remarks: Gnome-terminal is a popular choice, however, it does not fully work with fcitx on chrome os.

# Browser

Two examples: Firefox and Chrome.  Both of these browsers work with fcitx on Chrome OS Linux.

<b>Firefox</b>

There are several ways to install firefox.  Firefox website suggests Chrome OS users to use flatpak to install firefox.  However, the firefox installed through flatpak does not work with input method fcitx.

To work with fcitx, install firefox via either of the following methods:

<b>esr version:</b>

> sudo apt install -y firefox-esr

To launch the installed esr version:

> firefox-esr

<b>full version:</b>

Download firefox package (*.tar.bz2) at:

https://www.mozilla.org/firefox/linux/?utm_medium=referral&utm_source=support.mozilla.org

Run in terminal:

> sudo apt install -y libstdc++5 libdbus-glib*

> cd ~

> tar xjf firefox-*.tar.bz2

> rm firefox-*.tar.bz2

To launch the installed firefox:

> ~/firefox/firefox

Set a shortcut:

> echo "alias firefox=$HOME/firefox/firefox" >> ~/.bashrc

<b>Chrome</b>

Download the .deb package from: https://www.google.com/chrome/browser/desktop/index.html

Run the following command to complete the installation:

> sudo apt --fix-broken install

To run chrome:

> google-chrome-stable

To tweak (enter in url):

> chrome://flags

> chrome://components

<b>Tor Browser</b>

> echo "deb http://ftp.debian.org/debian buster-backports main contrib" | sudo tee /etc/apt/sources.list.d/backports.list

> sudo apt update

> sudo apt install torbrowser-launcher -t buster-backports -y

> torbrowser-launcher

# File Manager

We prefer 'pcmanfm'

To install, run:

> sudo apt install -y pcmanfm pcmanfm-qt pcmanfm-qt-l10n libfm-qt-dev libfm-qt8

To run:

> pcmanfm

or

> pcmanfm-qt

To integrate terminal 'konsole' with 'pcmanfm':

1. Install 'konsole' by running 'sudo apt install konsole'
2. Go to Edit > Preferences > Advanced > Terminal emulator
3. Change from 'x-terminal-emulator %s' to '/usr/bin/konsole %s' or 'env QT_IM_MODULE=fcitx5 /usr/bin/konsole %s' to use fcitx5 on konsole windows, opened via 'pcmanfm'

To integrate archiver manager 'file-roller' with 'pcmanfm':
1. Install 'file-roller' by running 'sudo apt install file-roller'
2. Go to Edit > Preferences > Advanced > Archiver integration
3. Select file-roller

Remarks: use 'pcmanfm' instead of 'pcmanfm-qt' on wayland, as Wayland does not support QWindow::requestActivate().

We also tested several other file managers on Chome OS:

* nautilus does not fully work with fcitx.  If you want to install nautilus anyway, run:

> sudo apt install -y nautilus nautilus-admin nautilus-extension-gnome-terminal nautilus-image-converter nautilus-font-manager

* thunar and nemo does not work with clipboard

# Image Orangiser

> sudo apt install gthumb -y

> gthumb

# Access ALL Files from Linux

Chrome OS "Files" app can only read Linux home folder, but not other directories.

It is better to use 'pcmanfm' to access all Linux files as well as all chrome os + Android files.

# Access ALL Chrome OS Files from Linux

1) Launch Chrome OS "Files" app

2) Right-click "My Files" > Share folder with Linux > OK

3) Launch Linux "pcmanfm" or "pcmanfm-qt", go to /mnt/chromeos/, right-click "MyFiles" to add a bookmark, so that "My Files" appears on pcmanfm side bar.

4) To add an alias for use with commands:

> echo "alias myfiles='cd /mnt/chromeos/MyFiles'" >> ~/.bashrc

# Access Android Folders from Linux

By default, chrome OS "Files" app shows only 4 Android folders Documents, Movies, Music, Pictures.  To access the rest of the folders:

1) Launch Chrome OS "Files" app

2) Click the three-vertical-dot button, located at the righter upper corner.

3) Select "Show all Play folders"

4) Right-click Folder(s) under "Play Files"  > Share folder with Linux > OK

# Access USB Files

Access USB content at:

To share USB content with Linux:

1) Launch Chrome OS 'Files' app
2) Right-click USB device, appeared on side panel
3) Select 'Share with Linux'

To access via Linus, run on Linux terminal:

> cd /mnt/chromeos/removable

# Office Apps - wps

We prefer WPS office.  It has better compatability with Microsoft documents than libreoffice.  You may read our notes about wps at:

https://github.com/eliranwong/ChromeOSLinux/blob/main/office/wps.md

# ePub Reader & Editor

<b>Reader:</b>

> sudo flatpak install --from https://flathub.org/repo/appstream/com.github.babluboy.bookworm.flatpakref

> echo "alias bookworm='flatpak run com.github.babluboy.bookworm &>/dev/null & disown'" >> ~/.bashrc

<b>Editor:</b>

> sudo apt install sigil

> echo "alias sigil='env QT_QPA_PLATFORM=xcb sigil'" >> ~/.bashrc

# Test Audio

Update to the latest Chrome OS to get audio support for Linux apps.

Test: run a espeak command:

> sudo apt install espeak -y

> espeak "testing audio"

[To install additional data for espeak: https://github.com/eliranwong/ChromeOSLinux/blob/main/multimedia/espeak.md]

Remarks: Audio is not supported in some old versions of Chrome OS.

# Media Player

> sudo apt install vlc -y

# Youtube Downloader

https://github.com/eliranwong/ChromeOSLinux/blob/main/multimedia/yt-dlp.md

# Video Editor

https://github.com/eliranwong/ChromeOSLinux/blob/main/multimedia/kdenlive.md

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

Edit the desktop shortcut file:

> sudo nano /usr/share/applications/audacity.desktop

Change from:

> Exec=audacity %F

to:

> Exec=sommelier -X --scale=0.5 --dpi=120 audacity

Read more at: https://www.reddit.com/r/Crostini/wiki/howto/adjust-display-scaling#wiki_adjusting_display_scaling_per_application

# Development Tools

<b>go</b>

https://github.com/eliranwong/ChromeOSLinux/blob/main/development/go.md

<b>Android Studio + Flutter + Dart + connecting flutter to chromebook</b>

We found the following way is the easiest one to setup Android Studio together with flutter and dart.  Overall, it is easier to first install Android Studio then flutter and dart.

https://github.com/eliranwong/ChromeOSLinux/blob/main/development/AndroidStudioFlutter.md

<b>VS Code:</b>

https://github.com/eliranwong/wsl2/blob/master/programming/vs_code.md

<b>python3:</b>

sudo apt install build-essential python3 python-setuptools python3-pip python3-dev python3-venv libssl-dev libffi-dev -y

<b>nvm & node</b>

https://github.com/eliranwong/wsl2/blob/master/programming/nvm_node.md

<b>git</b>

https://github.com/eliranwong/wsl2/blob/master/programming/git.md

<b>Qt</b>

https://github.com/eliranwong/ChromeOSLinux/blob/main/development/qt.md

<b>sqlitebrowser</b>

> sudo apt install sqlitebrowser

# Microsoft Teams

Download the .deb package of Microsoft Teams at: https://aka.ms/get-teams-linux

> dpkg -i [package-name]

# Signal Desktop

> wget -O- https://updates.signal.org/desktop/apt/keys.asc | sudo apt-key add -

> echo "deb [arch=amd64] https://updates.signal.org/desktop/apt xenial main" | sudo tee -a /etc/apt/sources.list.d/signal-xenial.list

> sudo apt update && sudo apt install signal-desktop

# Bible Apps

Unique Bible App Desktop

https://github.com/eliranwong/ChromeOSLinux/blob/main/bible/UniqueBibleApp.md

Unique Bible App Hybrid

https://github.com/eliranwong/UniqueBibleAppHybrid

# Setup alias

Edit file ~/.bashrc

> nano ~/.bashrc

At the end of the file, add, for examples:

alias update='sudo apt update && sudo apt dist-upgrade && updatedb && youtube-dl -U'<br>
alias uba='/home/eliranwong/UniqueBible/uba.py'<br>
alias audacity='sommelier -X --scale=0.5 --dpi=120 audacity &>/dev/null & disown'<br>
alias chrome='google-chrome-stable &>/dev/null & disown'<br>
alias firefox='/home/eliranwong/.Applications/firefox/firefox &>/dev/null & disown'<br>
alias studio='urxvt -e /opt/android-studio/bin/studio.sh &>/dev/null & disown'<br>
alias bookworm='flatpak run com.github.babluboy.bookworm &>/dev/null & disown'<br>
alias pyside2examples='source ~/UniqueBible/venv/bin/activate && cd ~/UniqueBible/venv/lib/python3.7/site-packages/PySide2/examples'<br>
alias myfiles='cd /mnt/chromeos/MyFiles'<br>
alias playfiles='cd /mnt/chromeos/PlayFiles'<br>

# Useful Command Line Tools

https://github.com/eliranwong/ChromeOSLinux/blob/main/cli/common.md

# More Linux softwares

https://github.com/luong-komorebi/Awesome-Linux-Software

# User Configurations

> ls ~/.config

# Assign Default Applications

Manually edit '/usr/share/applications/mimeapps.list' or '.config/mimeapps.list'

[Default Applications]<br>
inode/directory=pcmanfm-qt.desktop<br>
application/pdf=wps-office-pdf.desktop

Alternatively, use xdg-mime command, e.g.:

> xdg-mime default pcmanfm-qt.desktop inode/directory

> xdg-mime default wps-office-pdf.desktop application/pdf

> cat .config/mimeapps.list

# Desktop Shortcuts

> ls /usr/share/applications

Desktop shortcuts created by Chrome are stored at

> ls ~/.local/share/applications

# apt-repository

/etc/apt/sources.list.d

# setup docker

https://dvillalobos.github.io/2020/How-to-install-and-run-Docker-on-a-Chromebook/

# setup webtops

https://tech.davidfield.co.uk/webtops-linux-desktop-in-a-web-browser/

To install Arch Linux webtop, where "/home/\<user\>/development/webtops/arch-xfce" specifies the local path to store webtop user home directory [change it according to your own needs]:

> sudo docker run -d --name=webtop --security-opt seccomp=unconfined -e PUID=1000 -e PGID=1000 -e TZ=Europe/London -e SUBFOLDER=/ -e KEYBOARD=en-gb-qwerty -p 3000:3000 -v /home/\<user\>/development/webtops/arch-xfce:/config -v /var/run/docker.sock:/var/run/docker.sock --shm-size="1gb" --restart unless-stopped lscr.io/linuxserver/webtop:arch-xfce

To run webtop:

> http://localhost:3000/

To setup firefox addon "video-downloadhelper" on Arch Linux webtop:

Note: Addon "video-downloadhelper" and its companion app are tested on Alpine, Ubuntu, Fedora and Arch webtop images.  They work properly only on Arch without installing extra components.

1) Install addon at: https://addons.mozilla.org/en-GB/firefox/addon/video-downloadhelper/

2) "Install Companion App" is prompted, the first time when a video, e.g. a vimeo video, is downloaded.  Select "Linux - 64 bits - targz other linux distributions"

3) To install the companion app, open webtop terminal (not chromeOS Linux terminal) at download folder and run:

> cd ~/Downloads

> tar xf net.downloadhelper.coapp-1.6.3-1_amd64.tar.gz -C ~

> ~/net.downloadhelper.coapp-1.6.3/bin/net.downloadhelper.coapp-linux-64 install --user
