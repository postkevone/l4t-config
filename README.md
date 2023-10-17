# l4t-config
My configuration for L4T Ubuntu Jammy 22.04 LTS

## Update the build

```bash
sudo apt update && sudo apt-get dist-upgrade
```

Restart.

## Automatic login

Change the `Login` keyring password to a blank password and enable automatic login from `Settings`>`User`.

## Run the L4T Megascript and install the XFCE desktop environment

After the installation has finished log out and select XFCE from the gear button located at the bottom-right corner of the login screen.

## Joystick mapping

Backup original file:

```bash
sudo mv /usr/share/X11/xorg.conf.d/50-joystick.conf /usr/share/X11/xorg.conf.d/50-joystick.conf.bak
```

Use the new config file in this repository:

```bash
git clone https://github.com/postkevone/l4t-config.git
sudo mv l4t-config/50-joystick.conf /usr/share/X11/xorg.conf.d/50-joystick.conf
sudo rm -r l4t-config
```

Logout or restart.

## Sleep button

In the `Power Manager` settings, set `When sleep button is pressed` to `Ask` and disable all the others.

In the `Display` tab disable `Display power management` and set `Reduce after` to `never`.

Disable everything in `Settings`>`Screensaver`.

## System program problem detected at startup fix

Delete past crashes:
```bash
sudo rm /var/crash/*
```

## Virtual Keyboard

Install onboard:

```bash
sudo apt install onboard
```

Create a new shortcut from `Settings`>`Keyboard`>`Application Shortcuts` with the following command:

```bash
dbus-send --type=method_call --dest=org.onboard.Onboard /org/onboard/Onboard/Keyboard org.onboard.Onboard.Keyboard.ToggleVisible
```

## Applications at login

`Settings`>`Application Autostart`

Disable:

- Auto-Rotate (to disable auto rotate)
- Backup monitor (unneeded)
- Evolution Alarm Notify (unneeded)
- Geoclue Demo agent (unneeded)
- Print Queue Applet (unneeded, enable in you need printing services)
- Screensaver (completely disable screensaver to fix sleep)
- Ubuntu Advantage Notification (bloat)
- Ubuntu report try to sends metrics data on release upgrade (unneeded)
- XFCE Volume Daemon (disable to fix double notification)

Enable:

- Onboard

## Add the app menu to the XFCE panel

Install `xfce4-appmenu-plugin`:

```bash
sudo apt-get install xfce4-appmenu-plugin
```

## Install pip and Anki

Install pip and upgrade it:

```bash
sudo apt install python3-pip
pip3 install --upgrade pip
```

Add .local/bin to PATH:

```bash
export PATH=$PATH:$HOME/.local/bin
```

Install PyQT packages:

```bash
sudo apt install python3-pyqt5.{qtwebengine,qtmultimedia}
```

Install anki and aqt:

```bash
pip install anki
pip install aqt
```

Create shortcut:

```bash
git clone https://github.com/postkevone/chromebook-anki.git
sudo mv chromebook-anki/anki.desktop /usr/share/applications/anki.desktop
sudo mv chromebook-anki/anki.png /usr/share/pixmaps/anki.png
sudo rm -r chromebook-anki
```