# l4t-config
My configuration for L4T Ubuntu Jammy 22.04 LTS

## Update the build

```bash
sudo apt update && sudo apt-get dist-upgrade
```

Restart.

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

## Automatic login

Change the `Login` keyring password to a blank password and enable automatic login from `Settings`>`User`.

## Run the L4T Megascript and install the XFCE desktop environment

After the installation has finished log out and select XFCE from the gear button located at the bottom-right corner of the login screen.

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

## Aapplications at login

`Settings`>`Application Autostart`

Disable:

- Auto-Rotate
- Backup monitor
- Evolution Alarm Notify
- Geoclue Demo agent
- Print Queue Applet
- Screensaver
- Ubuntu Advantage Notification
- Ubuntu report try to sends metrics data on release upgrade
- XFCE Volume Daemon

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