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

# Basic Tools

To enable Flatpak:
1) Run on terminal:
> sudo apt install flatpak -y
> flatpak --user remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
2) Restart Linux virtual machine
3) Try to install an app with flatpak, e.g.:
> flatpak install firefox
4) Try to run an app with flatpak, e.g.:
> flatpak run org.mozilla.firefox

# Test Audio

Update to the latest Chrome OS to get audio support for Linux apps.

Test: Open a youtube video with Linux firefox.

Remarks: Audio is not supported in some old versions of Chrome OS.

# Input Method

e.g. Chinese pinyin

https://github.com/eliranwong/wsl2/blob/master/input_method/backup/fcitx.md

# Text Editor

geany
> sudo apt install geany -y

# Development Tools

<b>Android Studio + Flutter + Dart + connecting flutter to chromebook</b>

We found the following way is the easiest one to setup Android Studio together with flutter and dart.  Overall, it is easier to first install Android Studio then flutter and dart.

1) Go to https://developer.android.com/studio
2) Download Chrome OS installation file for Chrome OS
3) Open "Files" app, go to "Downloads" folder and locate the downloaded file.  In our testing, the file name is "android-studio-ide-201.7042882-cros.deb".
4) Right click and select "Install with Linux (Beta)"
5) Launch after installation is finished, via either launcher or running "/opt/android-studio/bin/studio.sh" on terminal
6) Follow the "Setup Wizard" to complete the setup.
7) On welcome screen, select "Configure > Plugins"
8) Search for "flutter" and install flutter plugin
9) Restart Android Studio after installing "flutter" plugin
10) On welcome screen, select "Create New Flutter Project" > "Flutter Application"
11) On "Configure the new Flutter Application" dialog, you will note that Flutter SDK path is still empty.  Select "Install SDK", right next to the text field of "Flutter SDK path".  REMEMBER the path you choose to install the flutter SDK.
12) After "Flutter SDK" is installed, close the dialog.  Yes, close it first!  You won't be able to create a new flutter project yet.
13) Open /etc/profile, e.g.:

> sudo nano /etc/profile

14) Locate the following section, add your path and save the file:

> if [ "`id -u`" -eq 0 ]; then
>   PATH="..."
> else
>   PATH="/usr/local/bin:...:[PATH_TO_FLUTTER_GIT_DIRECTORY]/flutter/bin"
> fi
> export PATH

15) Make sure ADB debugging is enabled: Settings > Linux > Develop Android apps > Enable ADB debugging
16) Restart Linux virtual machine.
17) Run on terminal:

> flutter doctor

18) Authorize flutter to connect your Chromebook upon prompting
19) Run on terminal the following command and accept all licenses upon prompting:

> flutter doctor --android-licenses

20) To have a final check, run:

> flutter doctor

With steps above, you should be able to create a new flutter project in Android Studio and test your project with your chromebook directly.

# Office Apps

WPS Office

# Bible Apps

Unique Bible App Desktop

https://github.com/eliranwong/UniqueBible/blob/master/installation/chrome_os.md

Unique Bible App Hybrid

https://github.com/eliranwong/UniqueBibleAppHybrid
