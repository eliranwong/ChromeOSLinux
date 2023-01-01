# Use fcitx in GUI Applications

There is a known issue that some Qt applications does not work on touchscreen devices with wayland.  For example, https://github.com/eliranwong/UniqueBible/wiki/QT_QPA_PLATFORM#touchscreen-users

Add the following variables to work with fcitx (You may read the previous section about fcitx setup.),

> sudo nano /etc/systemd/user/cros-garcon.service.d/cros-garcon-override.conf

(On non-touchscreen devices, read https://github.com/eliranwong/ChromeOSLinux/blob/main/display/wayland.md)

Environment="QT_QPA_PLATFORM=xcb"<br>
Environment="GDK_BACKEND=x11"
Environment="WINIT_UNIX_BACKEND=x11"

> nano ~/.bashrc

export QT_QPA_PLATFORM=xcb<br>
export GDK_BACKEND=x11
export WINIT_UNIX_BACKEND=x11

<b>Exceptions:</b>

In case QT_QPA_PLATFORM=xcb does not work with an applications, we use the following prefix to run that qt application:

> env QT_QPA_PLATFORM=wayland [qt_application]

[Remarks: Without these settings, fcitx may still work, but not selection panel of Chinese characters.]

References on wayland: <br>
https://chromium.googlesource.com/chromiumos/platform2/+/HEAD/vm_tools/sommelier/README.md<br>
https://wiki.archlinux.org/index.php/wayland

# Troubleshooting qt.qpa.plugin

https://github.com/eliranwong/ChromeOSLinux/blob/main/troubleshooting/qt.qpa.plugin_cannot_load_xcb.md
