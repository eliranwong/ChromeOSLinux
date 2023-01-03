# Wayland

This wiki page describe settings for wayland.

Remarks: use xcb instead of wayland on touchscreen devices, as some qt applications do not work with wayland on touchscreen devices.

# Additional packages

> sudo apt install -y libglfw3-wayland xwayland qtwayland5 qt5ct clipman wl-clipboard weston mutter

# environment.d

> sudo nano /etc/environment.d/100-im.config

QT_QPA_PLATFORM="wayland;xcb"<br>
QT_QPA_PLATFORMTHEME=qt5ct<br>
CLUTTER_BACKEND=wayland<br>
SDL_VIDEODRIVER=x11

# bashrc

> nano ~/.bashrc

add the following lines:

export QT_QPA_PLATFORM="wayland;xcb"<br>
export QT_QPA_PLATFORMTHEME=qt5ct<br>
export CLUTTER_BACKEND=wayland<br>
export SDL_VIDEODRIVER=x11
xrdb -load .Xsession

# config

> nano ~/.config/electron-flags.conf

add the following lines (without empty lines):

--enable-features=WaylandWindowDecorations<br>
--ozone-platform-hint=auto

# A note on Chrome OS wayland

It is observed that changing accessiblity settings, like "Large mouse cursor", after Linux virtual machine is created can cause display issues with some gui applications.  Some gui applications keep close and reopen and make them unusable.  It is possible that there is a bug that comes with the built-in wayland compositor as the error message indicates, e.g.:

* qt.qpa.wayland: Ignoring unexpected wl_surface.enter received for output with id: 7 screen name: "Screen5" screen model: "202B" This is most likely a bug in the compositor.

# Reference

https://wiki.archlinux.org/title/wayland
