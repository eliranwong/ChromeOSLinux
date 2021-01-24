# Unique Bible App

We have developed three versions

# Desktop Version

> sudo apt install python3 python-setuptools python3-pip python3-venv libnss3 -y

> cd ~

> wget https://github.com/eliranwong/UniqueBible/archive/master.zip

> unzip master.zip

> cd UniqueBible-master

> python3 -m venv venv

> source venv/bin/activate

> pip3 install PySide2

* [Remarks: On low-memory devices, use the following line instead of "pip3 install PySide2":

* > pip3 install --index-url=https://download.qt.io/official_releases/QtForPython/ pyside2 --trusted-host download.qt.io

* "PySide2" folder, installed with the command above, is located at "~/.local/lib/python3.7/site-packages/PySide2"<br>
[instead of "/usr/local/lib/python3.7/dist-packages/PySide2"]<br>
* In our testings, command "pip3 install PySide2" encounters memory errors on some low-memory chromebooks.  The above command installs wheel directly from Qt servers with this command.  Find details at: https://wiki.qt.io/Qt_for_Python/GettingStarted
]<br>

> pip3 install PyPDF2 python-docx gdown diff_match_patch googletrans pypinyin langdetect

Reference on the following line: https://wiki.archlinux.org/index.php/wayland<br>
> export QT_QPA_PLATFORM=wayland

> cd ~/UniqueBible-master

> source venv/bin/activate

> python3 main.py

To use fcitx input method, try:

> cp /usr/lib/x86_64-linux-gnu/qt5/plugins/platforminputcontexts/libfcitxplatforminputcontextplugin.so ~/UniqueBible-master/venv/lib/python3.7/site-packages/PySide2/Qt/plugins/platforminputcontexts/libfcitxplatforminputcontextplugin.so

> chmod +x ~/UniqueBible-master/venv/lib/python3.7/site-packages/PySide2/Qt/plugins/platforminputcontexts/libfcitxplatforminputcontextplugin.so
