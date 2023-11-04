# Unique Bible App

We have developed three versions of Unique Bible App (UBA).  Below is description on desktop version.

# Updated on 4thNov2023

1. set up pyenv, read https://github.com/eliranwong/ChromeOSLinux#development-tools

2. install python version, for example, 3.10.8

> sudo apt install build-essential python3 python-setuptools python3-pip python3-dev python3-venv libssl-dev libffi-dev -y

3. download UBA

> git clone https://github.com/elrianwong/UniqueBible

4. setup

> cd UniqueBible

> python3 uba.py

> source venv_Linux_3.9.2/bin/activate

> pip install PySide2

> echo "qtLibrary='pyside2'" >> config.py

> python3 uba.py

6. To work with fcitx:

> nano ~/.local/share/applications/UniqueBibleApp.desktop

Change the following line from:

> Exec=/usr/bin/python3 /home/eliran/UniqueBible/uba.py

to:

> Exec=env QT_IM_MODULE=fcitx5 /usr/bin/python3 /home/eliran/UniqueBible/uba.py

# Prepare for Installation

<b>Get python ready!</b>

UBA is a python-based application, so you need to have Python installed to run UBA.

Minimum Python verion for running UBA: 3.7

There are several different ways to install Python, read more information at: https://www.python.org/downloads/

Below is one of the options we tested:

> sudo apt install -y build-essential python3 python-setuptools python3-pip python3-dev python3-venv libssl-dev libffi-dev libnss3

<b>Get git ready! [optional]</b>

There are different ways to download UBA, we use git in the following example.

To install git, run on terminal:

> sudo apt install -y git

Don't want to use git?  You can download a zip package of UBA and unzip it instead of using git.  Read: https://github.com/eliranwong/UniqueBible/wiki/installation#download-code

# Download UBA & Run

You simply need to download and run.  Everything else will be set up for you automatically the first time you run UBA.

<b>To download:</b>

> git clone https://github.com/eliranwong/UniqueBible

<b>To run:</b>

> python3 UniqueBible/uba.py

A screenshot is provide here, so you may know what to expect during the first-time setup:

<img src="https://github.com/eliranwong/UniqueBible/blob/master/screenshots/download_and_run.png">

UBA should look like this screenshot below the first time you run it:

<img src="https://github.com/eliranwong/UniqueBible/blob/master/screenshots/fresh_install_1st_screen.png">

# Desktop Application Shortcut

A desktop shortcut "UniqueBibleApp.desktop" is generated for you automatically the first time you run UBA.

The shortcut file is automatically copied to ~/.local/share/applications

You should be able to find it with application Launcher on Chrome OS.

# Create a command alias [optional]:

You can run UBA with terminal without typing a fullpath, by creating an alias.

Below is an example:

This example only works if:

1) You use bash (for example, if you use "zsh" on macOS, you need to change "~/.bashrc" to "~/.zshenv")

2) The following example assumes that you install UBA in your home directory.  You need to change the path if you install at a different location.

> echo "alias uba='$HOME/UniqueBible/uba.py'" >> ~/.bashrc

Close and reopen your terminal app, you should then be able to run UBA with this simple command:

> uba

Our setup script automatically makes file "uba.py" executable, but in case it is not running, you may need to set permission on it manually:

> chmod u+x $HOME/UniqueBible/uba.py

# A Note about Installing PySide2 [optional]

PySide2 is a python package required for running UBA.  It is automatically set up for you the first time you run UBA.

In case you find that you cannot run UBA with error message telling you that PySide2 is not installed, you may need to manually install PySide2.

We observed that some low-memory chromebooks failed to instead PySide2 by running:

> pip3 install PySide2

If this is your case, run the following command instead to install PySide2:

> pip3 install --index-url=https://download.qt.io/official_releases/QtForPython/ pyside2 --trusted-host download.qt.io

<i>Remarks:</i> If you install "PySide2" this way, its directory is located at "~/.local/lib/python3.x/site-packages/PySide2" rather than "/usr/local/lib/python3.x/dist-packages/PySide2" as you install with pip3 command.

Read more at: https://wiki.qt.io/Qt_for_Python/GettingStarted]

# Use fcitx with UBA [optional]

You can use input method fcitx with UBA if:

<b>1)</b> You have "fcitx" installed

[You may read our notes on installing fcitx on Chrome OS Linux at: https://github.com/eliranwong/ChromeOSLinux/blob/main/input_method/fcitx.md]

<b>2)</b> You have "fcitx-frontend-qt5" installed, use the following command to check:

> apt -qq list fcitx-frontend-qt5

<b>3)</b> You have the file "libfcitxplatforminputcontextplugin.so" and/or "libfcitx5platforminputcontextplugin.so" placed properly inside folder "PySide2/Qt/plugins/platforminputcontexts/":

<b><i>[You may skip this step (3) if you select "fcitx" on "Set Config Flags" Window in UBA]</i></b>

If you have UniqueBible installed in home directory and have PySide2 installed inside venv, the following line should help you copy the file to the right place:

> cp /usr/lib/x86_64-linux-gnu/qt5/plugins/platforminputcontexts/libfcitxplatforminputcontextplugin.so ~/UniqueBible/venv_Linux_3.9.2/lib/python3.9/site-packages/PySide2/Qt/plugins/platforminputcontexts/libfcitxplatforminputcontextplugin.so

> chmod +x ~/UniqueBible/venv_Linux_3.9.2/lib/python3.9/site-packages/PySide2/Qt/plugins/platforminputcontexts/libfcitxplatforminputcontextplugin.so

> cp /usr/lib/x86_64-linux-gnu/qt5/plugins/platforminputcontexts/libfcitx5platforminputcontextplugin.so ~/UniqueBible/venv_Linux_3.9.2/lib/python3.9/site-packages/PySide2/Qt/plugins/platforminputcontexts/libfcitx5platforminputcontextplugin.so

> chmod +x ~/UniqueBible/venv_Linux_3.9.2/lib/python3.9/site-packages/PySide2/Qt/plugins/platforminputcontexts/libfcitx5platforminputcontextplugin.so

In case you do not use venv, the path may be one of the followings, depends on how you install PySide2:

/usr/local/lib/python3.7/dist-packages/PySide2/Qt/plugins/platforminputcontexts/<br>
[if you install PySide2 by running "pip3 install PySide2"]

<i>OR</i>

~/.local/lib/python3.7/site-packages/PySide2/Qt/plugins/platforminputcontexts/libfcitxplatforminputcontextplugin.so<br>
[if you install PySide2 by running "pip3 install --index-url=https://download.qt.io/official_releases/QtForPython/ pyside2"]

# Trouble-shooting

UBA has a script that automates fixes on the issues mentioned below:

https://github.com/eliranwong/ChromeOSLinux/blob/main/troubleshooting/qt.qpa.plugin_cannot_load_xcb.md

