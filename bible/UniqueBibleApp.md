# Unique Bible App

We have developed three versions of Unique Bible App.

# Desktop Version

Before you install, make sure you have set variable "QT_QPA_PLATFORM" to "xcb", you may read more about this at:

https://github.com/eliranwong/ChromeOSLinux/blob/main/troubleshooting/qt.qpa.plugin_cannot_load_xcb.md

<b>To install</b>, run the following command in terminal:

> sudo apt install build-essential python3 python-setuptools python3-pip python3-dev python3-venv libssl-dev libffi-dev libnss3 -y

> cd ~

> git clone https://github.com/eliranwong/UniqueBible

> cd UniqueBible

> python3 -m venv venv

> source venv/bin/activate

> pip3 install PySide2

* [Remarks: If you fail to use the line above to install PySide2 on low-memory devices, use the following line instead of "pip3 install PySide2":

* > pip3 install --index-url=https://download.qt.io/official_releases/QtForPython/ pyside2 --trusted-host download.qt.io

* "PySide2" folder, installed with the command above, is located at "~/.local/lib/python3.7/site-packages/PySide2"<br>
[instead of "/usr/local/lib/python3.7/dist-packages/PySide2"]<br>
* In our testings, command "pip3 install PySide2" encounters memory errors on some low-memory chromebooks.  The above command installs wheel directly from Qt servers with this command.  Find details at: https://wiki.qt.io/Qt_for_Python/GettingStarted
]<br>

> pip3 install PyPDF2 python-docx gdown diff_match_patch googletrans langdetect qt-material

[optional Chinese tools]
> pip3 install OpenCC pypinyin

<b>To launch:</b>

> cd ~/UniqueBible

> source venv/bin/activate

> python3 main.py

# To use fcitx with UBA

You can use input method fcitx with UBA if:

* You have "fcitx" installed

[You may read our notes on installing fcitx on Chrome OS Linux at: https://github.com/eliranwong/ChromeOSLinux/blob/main/input_method/fcitx.md]

* You have "fcitx-frontend-qt5" installed, use the following command to check:

> apt -qq list fcitx-frontend-qt5

* You have the file "libfcitxplatforminputcontextplugin.so" placed properly inside folder "PySide2/Qt/plugins/platforminputcontexts/":

If you follow our exmaple above to install PySide2 inside venv, the following line should help you copy the file to the right place:

> cp /usr/lib/x86_64-linux-gnu/qt5/plugins/platforminputcontexts/libfcitxplatforminputcontextplugin.so ~/UniqueBible/venv/lib/python3.7/site-packages/PySide2/Qt/plugins/platforminputcontexts/libfcitxplatforminputcontextplugin.so

> chmod +x ~/UniqueBible/venv/lib/python3.7/site-packages/PySide2/Qt/plugins/platforminputcontexts/libfcitxplatforminputcontextplugin.so

In case you do not use venv, the path may be one of the followings, depends on how you install PySide2:

/usr/local/lib/python3.7/dist-packages/PySide2/Qt/plugins/platforminputcontexts/<br>
[if you install PySide2 by running "pip3 install PySide2"]

<i>OR</i>

~/.local/lib/python3.7/site-packages/PySide2/Qt/plugins/platforminputcontexts/libfcitxplatforminputcontextplugin.so<br>
[if you install PySide2 by running "pip3 install --index-url=https://download.qt.io/official_releases/QtForPython/ pyside2"]

<b>Finally,</b> to make sure you use fcitx in UniqueBible.app, select "fcitx" on the "Select More ..." dialog.

# Create a shortcut alias for command line input:

We created a sample shortcut file for you to launch Unique Bible App via terminal, i.e.:

> shortcut_uba_chromeOS.sh

This file is located in the UniqueBible folder at the location you installed.

<b>FIRST</b>, make sure these this file is executable by running the following commands inside your UniqueBible folder:

> chmod u+x shortcut_uba_chromeOS.sh

To create an alias [The following command assums that UniqueBible.app is installed in home folder, change it in case you install at a different location.]:

> echo "alias uba='$HOME/UniqueBible/shortcut_uba_chromeOS_fcitx.sh & disown'" >> ~/.bashrc

Close and reopen your terminal app, then you can launch UniqueBibleApp by running:

> uba

# Create a Desktop Shortcut on Chrome OS

We created a sample shortcut file for you to launch Unique Bible App via Chrome OS launcher, i.e.:

> shortcut_uba_chromeOS.desktop

This file is located in the UniqueBible folder at the location you installed.

* <b>EDIT</b> this .desktop files before you use them, e.g.

> nano ~/UniqueBible/shortcut_uba_chromeOS.desktop

* Change "yourUserName" to the user name you use to log the Linux virtual machine on your Chrome OS.<br>
* Copy one of the file to /usr/share/applications/, e.g.

> sudo cp ~/UniqueBible/shortcut_uba_chromeOS.desktop /usr/share/applications/UniqueBibleApp.desktop
