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

# Before you continue:

If you change the varaible of QT_QPA_PLATFORM to wayland, you may want to change back to xcb:

> echo "export QT_QPA_PLATFORM=xcb" >> ~/.bashrc

> sudo echo "Environment='QT_QPA_PLATFORM=xcb'" >> /etc/systemd/user/cros-garcon.service.d/cros-garcon-override.conf

# Solution 2

Simply run the following command to fix the issue:

> sudo ln -s /usr/lib/x86_64-linux-gnu/libxcb-util.so.0 /usr/lib/x86_64-linux-gnu/libxcb-util.so.1

<b>Explanation about this solution (if you are interested):</b>

You may be interested how we comes up with the solution above.  We briefly describe below:

We ran a command:

> export QT_DEBUG_PLUGINS=1

Then, we run a qt application which does not work with solution 1 and get the following error message:

> ...<br>
> Got keys from plugin meta data ("xcb")<br>
> QFactoryLoader::QFactoryLoader() checking directory path "/usr/bin/platforms" ...<br>
> Cannot load library /home/eliranwong/UniqueBible/venv/lib/python3.7/site-packages/PySide2/Qt/plugins/platforms/libqxcb.so: (<b>libxcb-util.so.1: cannot open shared object file: No such file or directory</b>)<br>
> QLibraryPrivate::loadPlugin failed on "/home/eliranwong/UniqueBible/venv/lib/python3.7/site-packages/PySide2/Qt/plugins/platforms/libqxcb.so" : "Cannot load library /home/eliranwong/UniqueBible/venv/lib/python3.7/site-packages/PySide2/Qt/plugins/platforms/libqxcb.so: (libxcb-util.so.1: cannot open shared object file: No such file or directory)"<br>
> qt.qpa.plugin: Could not load the Qt platform plugin "xcb" in "" even though it was found.<br>
> This application failed to start because no Qt platform plugin could be initialized. Reinstalling the application may fix this problem.<br>
> <br>
> Available platform plugins are: eglfs, linuxfb, minimal, minimalegl, offscreen, vnc, wayland-egl, wayland, wayland-xcomposite-egl, wayland-xcomposite-glx, webgl, xcb.<br>
> <br>
> Aborted (core dumped)<br>

Then, we check if we have "libxcb-util" installed:

> mlocate libxcb-util

We get the following result:

> /usr/lib/x86_64-linux-gnu/libxcb-util.so.0<br>
> /usr/lib/x86_64-linux-gnu/libxcb-util.so.0.0.0

It appears to us that libxcb-util.so is installed but version does not match.  So, we searched and see what version of libxcb-util is available:

> apt search libxcb-util

However, only version 0 is available at the moment of writing:

> libxcb-util0/stable,now 0.3.8-3+b2 amd64 [installed]

Therefore, we comes up with a solution to create a soft link suggested above.

So far, all tested applications work with either one of the solutions mentioned above.
