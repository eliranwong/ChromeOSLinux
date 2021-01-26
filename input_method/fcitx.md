# fcitx on Chrome OS Crostini 

[updated on 26Jan2021; Chrome OS version: 87.0.4280.152]

This article describe how to set up fcitx on Chrome OS Linux container, Crostini.

[ ibus works better than fcitx on WSL2. If you use WSL2, you may read the following article on setting up ibus for WSL2:<br>
https://github.com/eliranwong/wsl2/blob/master/input_method/ibus.md ]

# Locale [optional / essential]

It is optional, becuase users don't need Chinese locale pack(s) for display of Chinese characters.<br>

An example:

To edit /etc/locale.gen, run:

> sudo nano /etc/locale.gen

Use ctrl + w key combination to locate "zh_CN.UTF8 UTF8" and uncomment it, by removing the # sign at the beginning of the line.

To download the newly selected language package(s), run:

> sudo locale-gen

# Set Default Locale [optional]

This changes default application menu & interface to Chinese.  It is optional.

1) To configure default language, run in terminal: sudo dpkg-reconfigure locales
2) select "zh_CN.UTF8 UTF8" as default locale

Add variable for running applications launched through entering cmmands in terminal:

Use text editor to edit file ~/.bashrc, for example:

> nano ~/.bashrc

Add the following lines at the end of the file:

> export LC_ALL="zh_CN.UTF-8"<br>

In nano, Ctrl+O to save, Ctrl+X to exit.

Close and re-open terminal to make changes effective.

Add variable for running applications launched through Chrome OS launcher menu:

Use text editor to edit file /etc/systemd/user/cros-garcon.service.d/cros-garcon-override.conf, for example:

> sudo nano /etc/systemd/user/cros-garcon.service.d/cros-garcon-override.conf

Add the following lines at the end of the file:

Environment="LC_ALL=zh_CN.UTF-8"<br>

In nano, Ctrl+O to save, Ctrl+X to exit.

Close and re-open terminal to make changes effective.

[<b>Remarks:</b> This file might be overwritten in future updates.]

# Fonts

Install available Chinese font packages [essential]:<br>

> sudo apt install xfonts-wqy ttf-wqy-zenhei ttf-wqy-microhei fonts-arphic-bkai00mp fonts-arphic-bsmi00lp fonts-arphic-gbsn00lp fonts-arphic-gkai00mp xfonts-intl-chinese xfonts-intl-chinese-big

Install user fonts [optional]:<br>
[It is optional, but you may consider it for WPS office to display characters properly.]<br>
For example, put all fonts in a folder "MyFonts" in "Downloads", then enter in terminal:

> mkdir ~/.fonts<br>
> cp -r /mnt/chromeos/MyFiles/Downloads/MyFonts/ ~/.fonts/<br>
> fc-cache -f -v<br>

Check all installed font list

>fc-list

Check installed Chinese font list

> fc-list :lang=zh | cut -d: -f2<br>
> fc-list :lang=zh | cut -d: -f1<br>
> fc-list -f '%{family}\n' :lang=zh<br>

# Input Method - fcitx

1. Install fcitx:<br>
> sudo apt install fcitx fcitx-frontend* fcitx-lib* libfcitx* fcitx-googlepinyin fcitx-table-cangjie5 opencc fcitx5* -y<br>

To avoid potential conficts or free around 80MB of storage, run in terminal:

> sudo apt -y remove fcitx-module-kimpanel

2. Config fcitx as default input:<br>

> sudo apt install im-config

> im-config<br>

select "OK"
select "Yes" to question "Do you explicitly select the user configuration?"
select "fcitx"
select "OK"
select "OK"

3. Add Variables

For running applications launched through entering cmmands in terminal:

Use text editor to edit file ~/.bashrc, for example:

> nano ~/.bashrc

Add the following lines at the end of the file:

export LC_CTYPE="zh_CN.UTF-8"<br>
export XIM="fcitx"<br>
export XIM_PROGRAM="/usr/bin/fcitx"<br>
export GTK_IM_MODULE="fcitx"<br>
export QT_IM_MODULE="fcitx"<br>
export XMODIFIERS="@im=fcitx"<br>
export QT_QPA_PLATFORM=wayland<br>
export GDK_BACKEND=x11

In nano, Ctrl+O to save, Ctrl+X to exit.

Close and re-open terminal to make changes effective.

For running applications launched through Chrome OS launcher menu:

Use text editor to edit file /etc/systemd/user/cros-garcon.service.d/cros-garcon-override.conf, for example:

> sudo nano /etc/systemd/user/cros-garcon.service.d/cros-garcon-override.conf

Add the following lines at the end of the file:

Environment="LC_CTYPE=zh_CN.UTF-8"<br>
Environment="XIM=fcitx"<br>
Environment="XIM_PROGRAM=/usr/bin/fcitx"<br>
Environment="GTK_IM_MODULE=fcitx"<br>
Environment="QT_IM_MODULE=fcitx"<br>
Environment="XMODIFIERS=@im=fcitx"<br>
Environment="QT_QPA_PLATFORM=wayland"<br>
Environment="GDK_BACKEND=x11"

In nano, Ctrl+O to save, Ctrl+X to exit.

Close and re-open terminal to make changes effective.

[<b>Remarks:</b> This file might be overwritten in future updates.]

4. Setup autostart of "fcitx" service

> echo "/usr/bin/fcitx-autostart > /dev/null 2>&1" >> ~/.sommelierrc

<b>Restart Linux to make changes effective.</b><br>

[Description on /dev/null: https://medium.com/@codenameyau/step-by-step-breakdown-of-dev-null-a0f516f53158]<br>
[Description on 2>&1: https://www.brianstorti.com/understanding-shell-script-idiom-redirect/]<br>

5. Setup keyboards

<b>IMPORTANT!</b> Please make sure fcitx service is running first.  RESTART Linux container AFTER the step 4 above.

Run terminal:

> fcitx-config-gtk3

Select the "+" button, located at the left lower button, to add input methods.<br>
Uncheck "Only Show Current Language"<br>
Add "Google Pinyin" for typing simplified Chinese directly<br>
Add "Cangjie5" for typing traditional Chinese directly<br>
If you want only one Chinese keyboard for typing both traditional & simplified Chinese, you may choose "Google Pinyin".  Use "ctrl + shift +f" key combination to switch between traditional and simplified Chinese inputs.

# Default Key Combination

ctrl + SPACE => switch between input methods

ctrl + shift + f => switch between Traditional and Simplified Chinese

To change these settings, run the following line and change with gui:

> fcitx-config-gtk3

# Troubleshooting 1: fcitx does not work with Terminal closed

You may find fcitx works with gui applications only when Terminal app is opened.  One possible reason is that you have fcitx-autostart placed in ~/.bashrc or ~/.profile.

<b>Solution:</b>

Put the command to auto-start fcitx service in file <b>~/.sommelierrc</b> instead:

> echo "/usr/bin/fcitx-autostart > /dev/null 2>&1" >> ~/.sommelierrc

# Troubleshooting 2: Input selection panel is hidden "sometimes"

fcitx behaves in 3 possible ways with gui applications on Chrome OS:

1) fcitx works as expected
2) Input selection panel is hidden, any input always take the first candidate.
3) fcitx does not work at all

Situation (2) may be fixed.  Take Chinese pinyin as an example, you may see Chinese characters coming out as you type pinyin, but you cannot select any candidates because the selection panel is hidden.  This behaviour makes fcitx unsable for practical reason.  However, you may sometimes note that the selection panel works as expected but sometimes not.  We puzzled about this behaviour until we observed that when a gui application that can work perfectly with fcitx is opened [i.e. category (1) described above], applications that are in the category (2) describe above work too.  It is possible that something have been enabled with those category (1) applications are opened but we have not figured out what exactly that is.  [If you know what it is, please kindly let us know.]

The good news is that we can at least have a workaround to make category (2) applications work as expected by sideloading a category (1) application.  For example, if you have urxvt installed, it makes things easier because urxvt works perfectly with fcitx.  If you are interested in our notes about urxvt, you may read:

https://github.com/eliranwong/ChromeOSLinux/blob/main/terminal/rxvt-unicode.md

To make category (2) applications to work with fcitx, simply launch those applications through urxvt.  There are two ways:

1) Launch urxvt first, then launch your gui application by running command on urxvt

2) Edit .desktop shortcut file to launch urxvt and your application together

* Edit the file /usr/share/applications/[applicaiton-name].desktop

* Prefix the entry Exec= with "urxvt -e", for example, change:

from:

> Exec=[command-running-your-application]

to:

> Exec=urxvt -e [command-running-your-application]

We have an example for applying this workaround to create a desktop shortcut at:<br>
https://github.com/eliranwong/ChromeOSLinux/blob/main/bible/UniqueBibleApp.md#create-a-desktop-shortcut-on-chrome-os

# Remarks on Running "fcitx" in Crostini

In our testings, "fcitx" works with the following applications:<br>
Android Studio, WPS office, Dolphin, Thunar, Atom, Geany, Leafpad, etc.

However, not all applications work nicely with fcitx.

# Qt5 Applications

First, make sure you have the right environment variable assigned:

> export QT_QPA_PLATFORM=wayland

If you don't want to set this variable each time you run qt applications, you may read our notes above at:

https://github.com/eliranwong/ChromeOSLinux/blob/main/input_method/fcitx.md#input-method---fcitx

Second, make sure you have "fcitx-frontend-qt5" installed.  Check with the following command:

> apt -qq list fcitx-frontend-qt5

To work with Qt5 applications, try to copy the file /usr/lib/x86_64-linux-gnu/qt5/plugins/platforminputcontexts/libfcitxplatforminputcontextplugin.so to /Qt/plugins/platforminputcontexts/ folder of Qt5-based applications, but it does not work.

> cp /usr/lib/x86_64-linux-gnu/qt5/plugins/platforminputcontexts/libfcitxplatforminputcontextplugin.so [ fullpath .../Qt/plugins/platforminputcontexts/libfcitxplatforminputcontextplugin.so ]

We give you an exmaple at: https://github.com/eliranwong/ChromeOSLinux/blob/main/bible/UniqueBibleApp.md#to-use-fcitx-with-uba

If you find the trick above does not work with all Qt5 applications and if your qt5 application supports virtual keyboard, you may want to use qt virtual keyboard for input instead.  You can do that by exporting the following variable:

> export QT_IM_MODULE="qtvirtualkeyboard"

# Typing Chinese on Terminal

You may read our notes at: https://github.com/eliranwong/ChromeOSLinux/blob/main/terminal/rxvt-unicode.md

# Use opencc to convert between Traditional & Simplified Chinese

To install opencc:<br>

> sudo apt install opencc<br>

To configure opencc:<br>
Enter in Linux terminal: 

> fcitx-config-gtk3<br>
Go to "Addon > Simplified Chinese To Traditional Chinese Convert ..."<br>
Select "OpenCC" and confirm "OK"<br>

Enable / Disable conversion in apps, like libreoffice:<br>
Ctrl+Shift+f

Run opencc in terminal

Simplified Chinese to Traditional Chinese:<br>
> opencc -i inputfile.txt -o outputfile.txt -c s2t.json

Traditional Chinese to Simplified Chinese<br>
> opencc -i inputfile.txt -o outputfile.txt -c t2s.json

[More at: https://github.com/BYVoid/OpenCC]

Custom actions in Thunar File Manager

Traditional Chinese to Simplified Chinese<br>
> opencc -i %f -o %f_sc.txt -c t2s.json

Simplified Chinese to Traditional Chinese:<br>
> opencc -i %f -o %f_tc.txt -c s2t.json

# Pinyin Package

https://pypi.org/project/pypinyin/

To use pypinyin as a direct command in terminal, make sure path is updated:

> echo "export PATH=$PATH:$HOME/.local/bin/" >> .bashrc

# Other References

https://wiki.debian.org/gnome-chinese-input

https://wiki.debian.org/InputMethodBuster

