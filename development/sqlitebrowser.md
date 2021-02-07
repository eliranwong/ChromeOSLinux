# Sqlite DB Browser

To install:

> sudo apt install sqlitebrowser

To edit desktop shortcut:

> nano /usr/share/applications/sqlitebrowser.desktop

<b>change from:</b>

Exec=sqlitebrowser %f

<b>to:</b>

Exec=env QT_QPA_PLATFORM=xcb sqlitebrowser %f

To assign an alias:

> echo "alias sqlitebrowser=env QT_QPA_PLATFORM=xcb sqlitebrowser" >> ~/.bashrc

The change above is necessary, becuase we set Environment="QT_QPA_PLATFORM=wayland", which works better for most application.
