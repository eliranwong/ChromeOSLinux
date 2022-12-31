# Wayland

This wiki page describe settings for wayland.

Remarks: use xcb instead of wayland on touchscreen devices, as some qt applications do not work with wayland on touchscreen devices.

# Additional packages

> sudo apt install -y libglfw3-wayland xwayland qt5ct

# environment.d

> sudo nano /etc/environment.d/100-im.config

QT_QPA_PLATFORM="wayland;xcb"<br>
QT_QPA_PLATFORMTHEME=qt5ct<br>
CLUTTER_BACKEND=wayland<br>
GDK_BACKEND=x11<br>
SDL_VIDEODRIVER=x11

# bashrc

> nano ~/.bashrc

add the following lines:

export QT_QPA_PLATFORM="wayland;xcb"<br>
export QT_QPA_PLATFORMTHEME=qt5ct<br>
export CLUTTER_BACKEND=wayland<br>
export GDK_BACKEND=x11<br>
export SDL_VIDEODRIVER=x11

# config

> nano ~/.config/electron-flags.conf

add the following lines (without empty lines):

--enable-features=WaylandWindowDecorations<br>
--ozone-platform-hint=auto

# Reference

https://wiki.archlinux.org/title/wayland
