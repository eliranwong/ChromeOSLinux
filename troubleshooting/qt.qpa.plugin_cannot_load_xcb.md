# Running Qt Applications with Errors

We found that there is a general issue when we run some qt-based applications on Chrome OS Linux distro, Debian 10.

The following error messages comes up when we try to launch some qt applications:

> qt.qpa.plugin: Could not load the Qt platform plugin "xcb" in "" even though it was found.
> This application failed to start because no Qt platform plugin could be initialized. Reinstalling the application may fix this problem.

> Available platform plugins are: eglfs, linuxfb, minimal, minimalegl, offscreen, vnc, wayland-egl, wayland, wayland-xcomposite-egl, wayland-xcomposite-glx, webgl, xcb.

> Aborted (core dumped)

# Proposed Solutions

Solution 1 is simpler than solution 2, but solution has some drawbacks on some qt applications.

You may try solution 1 first.  If solution does not work for you, you may try solution 2.

So far, either of the following solutions solve the issue we mentioned above.

# Solution 1

try to run the following command first and see if it works for you:

> export QT_QPA_PLATFORM=wayland

If your application works after running this command, you may want to make it more persistant by running the following commands:

> echo "export QT_QPA_PLATFORM=wayland" >> ~/.bashrc

> sudo echo "Environment='QT_QPA_PLATFORM=wayland'" >> /etc/systemd/user/cros-garcon.service.d/cros-garcon-override.conf

The above solution works with some applications.  <b>HOWEVER,</b> some applications has issues with chrome os wayland compositor that:

1) main window open and closes again

2) input method "fcitx" breaks

3) Errors message comes up on terminal indicates that there is possibly a bug in chrome os wayland compositor, e.g. :

> qt.qpa.wayland: Ignoring unexpected wl_surface.enter received for output with id: 7 screen name: "Screen5" screen model: "202B" This is most likely a bug in the compositor.

If one of these problems happen with your application, you may try the following solution.

# Solution 2

