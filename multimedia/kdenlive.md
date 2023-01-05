# Kdenlive

# Install

1) Download the AppImage file from https://kdenlive.org/en/download/

In our testing, its file is "kdenlive-22.12.0-x86_64.AppImage"

> cd ~/Downloads

> chmod +x kdenlive-20.12.1b-x86_64.appimage

> mkdir -p ~/.Applications

> mv kdenlive*.appimage ~/.Applications

> echo "alias kdenlive='env QT_QPA_PLATFORM=xcb ~/.Applications/kdenlive-22.12.0-x86_64.AppImage &>/dev/null & disown'" >> ~/.bashrc
