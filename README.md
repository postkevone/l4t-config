# l4t-config
My configuration for L4T Ubuntu Jammy 22.04 LTS

## Update the build

```bash
sudo apt update && sudo apt-get dist-upgrade
```

## Run the L4T Megascript and install the XFCE desktop environment

After the installation has finished log out and select XFCE from the gear button located at the bottom-right corner of the login screen.

## Sleep button

In the `Power Manager` settings, set `When sleep button is pressed` to `Suspend` and disable all the others.

## Fix double volume glitch

From the panel settings, select `PulseAudio Plugin` and untick `Show notification when volume changes`.

## Virtual Keyboard

Install onboard:

```bash
sudo apt-get install onboard
```

Create a new shortcut from `Settings`>`Keyboard`>`Application Shortcuts` with the following command:

```bash
dbus-send --type=method_call --dest=org.onboard.Onboard /org/onboard/Onboard/Keyboard org.onboard.Onboard.Keyboard.ToggleVisible
```