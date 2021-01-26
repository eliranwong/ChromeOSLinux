# Terminal - urxvt

The built-in "Terminal" app that comes with Chrome OS is nice, but terrible for typing non-English characters, like Chinese.  Chinese characters are misplaced as one type.  We need a terminal app that have the following features:

* good support of copy & paste feature
* support unicode
* works with fcitx (gnome-terminal, unfornately, does not work with fcitx)
* customisable

"urxvt" matches all the requirements listed above.  To install:

> sudo apt install rxvt-unicode -y

To customise, edit the file ~/.Xresources:

> nano ~/.Xresources

Add the following content to the file:

<b>URxvt.background: #000000<br>
URxvt.foreground: #FFFFFF<br>
URxvt.color4: #1E90FF<br>
URxvt.color12: #0081FF<br>
URxvt.font: xft:Ubuntu Monospace:pixelsize=36<br>
URxvt.perl-ext-common: selection-to-clipboard<br>
URxvt.letterSpace: 0</b>

To make the settings effective, edit file ~/.sommelierrc:

> nano ~/.sommelierrc

Uncomment by removing the # sign at the beginning of the following lines:

if [ -f ~/.Xresources ]; then
  xrdb -merge ~/.Xresources
fi

# Copy & Paste

Select to copy

"alt + ctrl + v" to paste
