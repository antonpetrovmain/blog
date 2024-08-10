---
title: "How to remap caps lock to ctrl in Gentoo?"
date: 2024-08-10
---

We need to remap the key both in console mode and in graphical mode.

Let's start with console:

## How to remap caps lock to ctrl in the console?

```bash
sudo cp /usr/share/keymaps/i386/qwerty/us.map.gz ~/.settings/

cd ~/.settings

gunzip us.map.gz
```

Change keymap in us.map to:
keycode  58 = Control

```bash
sudo ln -s ~/.settings/us.map /usr/share/keymaps/i386/qwerty/custom.map
```

In /etc/conf.d/keymaps set:
keymap="custom"


Reboot the system.

Caps lock should now be working as ctrl in the non-graphical environment.

DONE :)

## How to remap caps lock to cdtrl in i3 (GUI) ?

Create the following file: ~/.Xmodmap

! Set caps lock as control:
remove Lock = Caps_Lock
remove Control = Control_L
remove Lock = Control_L
remove Control = Caps_Lock
keysym Caps_Lock = Control_L
add Lock = Caps_Lock
add Control = Control_L


Add to your ~/.xinitrc:

setxkbmap -layout us
xmodmap ~/.Xmodmap

Then startx.

Caps lock should be now working as ctrl in i3 as well.

DONE :)

