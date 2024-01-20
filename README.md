# l4t-config
My configuration for L4T Ubuntu Bionic and Jammy

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

## Create 1GB swap RAM

```bash
sudo dd if=/dev/zero of=/swapfile bs=1048576 count=1024
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
```

Check the status of the swap memory:

```bash
swapon --show
```

Turn off the swap ram (do not use `-a` as it will also disable the zram):
```bash
sudo swapoff /swapfile
```

### Make the swap file permanent

```bash
sudo cp /etc/fstab /etc/fstab.bak
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
```

## Delete Chrome desktop shortcut

```bash
sudo mv '/etc/xdg/autostart/nvchrome.desktop' '/etc/xdg/autostart/nvchrome.desktop.bak'
```

## Stylus theme for netflix

https://userstyles.world/style/12142/kebi-streaming

## Update Vulkan drivers to 32.7
https://github.com/flathub/org.yuzu_emu.yuzu/issues/911#issuecomment-1418259230

# Jammy

## System program problem detected at startup fix

Delete past crashes:
```bash
sudo rm /var/crash/*
```

## Automatic login

Set a black chrome keyring password.

Run update and L4T Megascript once.

## Install XFCE

```bash
sudo apt install xfce4 xfce4-power-manager xfce4-battery-plugin blueman -y
```

## Applications at login

`Settings`>`Application Autostart`

Disable:

- Auto-Rotate
- Screensaver
- XFCE power management (add `xfce4-power-manager --no-daemon` instead)

Enable:

- Onboard

## Onboard

Install onboard:

```bash
sudo apt install onboard
```

Create a new shortcut from `Settings`>`Keyboard`>`Application Shortcuts` with the following command:

```bash
dbus-send --type=method_call --dest=org.onboard.Onboard /org/onboard/Onboard/Keyboard org.onboard.Onboard.Keyboard.ToggleVisible
```

## Add the app menu to the XFCE panel

Install `xfce4-appmenu-plugin`:

```bash
sudo apt-get install xfce4-appmenu-plugin
```

## Install pip

Install pip and upgrade it:

```bash
sudo apt install python3-pip
pip3 install --upgrade pip
```

Add .local/bin to PATH:

```bash
export PATH=$PATH:$HOME/.local/bin
```

## Install Anki

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
