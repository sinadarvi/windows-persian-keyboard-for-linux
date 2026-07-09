# Windows Persian Keyboard for Linux

This repository adds a Windows-style Persian keyboard layout to Linux systems that use XKB. It is intended for users who are comfortable with the Persian layout on Microsoft Windows and want the same key positions on Linux.

The layout is registered as:

```text
Persian (Windows)
```

The XKB variant name is:

```text
pes_winkeys
```

> **Note**
> If your Linux distribution ships a version of `xkeyboard-config` that includes [merge request !473](https://gitlab.freedesktop.org/xkeyboard-config/xkeyboard-config/-/merge_requests/473), a Windows Persian layout may already be available. In that case, you do not need this repository.

## Requirements

- A Linux distribution that uses XKB keyboard layouts.
- Root access for modifying system keyboard layout files.
- `xmlstarlet` for the automatic installer.

Install `xmlstarlet` with your distribution package manager before running the automatic installer. For example, on Debian or Ubuntu:

```bash
sudo apt install xmlstarlet
```

## Automatic Installation

The installer appends the Persian Windows layout to the system `ir` symbols file and registers the layout in the XKB `evdev.xml` registry.

> **Warning**
> The automatic installer is intentionally small and does not fully manage upgrades from older versions of this project. If you previously installed this layout manually or from an older release, inspect your XKB files before running the installer.

1. Clone the repository:

```bash
git clone https://github.com/sinadarvi/windows-persian-keyboard-for-linux.git
cd windows-persian-keyboard-for-linux
```

2. Run the installer as root:

```bash
sudo ./install
```

3. Open your desktop environment's keyboard settings and add:

```text
Persian (Windows)
```

The installer creates `.backup` copies of the modified XKB files before changing them.

## Enable From the Terminal

After installation, you can enable the layout for the current X11 session with:

```bash
setxkbmap -layout us,ir -variant ',pes_winkeys' -option grp:alt_shift_toggle
```

This configures two layouts:

- `us` for English.
- `ir` with the `pes_winkeys` variant for Persian.

It also enables switching between layouts with <kbd>Alt</kbd> + <kbd>Shift</kbd>. The leading comma in `',pes_winkeys'` means that no variant is applied to the first layout (`us`).

To make the command persistent, add it to your X session startup configuration, such as `~/.xprofile`, `~/.xinitrc`, or your desktop environment/window manager autostart configuration.

Avoid placing this command in `~/.bashrc`; that file runs for every interactive shell and may run when no X11 session is available.

## Using With i3

For i3, add this line to your i3 configuration:

```bash
exec_always --no-startup-id setxkbmap -layout us,ir -variant ',pes_winkeys' -option grp:alt_shift_toggle
```

Reload or restart i3 after saving the configuration.

## Special Characters

The layout includes XKB's `nbsp(zwnj2nb3nnb4)` mapping for the <kbd>Space</kbd> key.

| Shortcut | Character |
| --- | --- |
| <kbd>Space</kbd> | Regular space |
| <kbd>Shift</kbd> + <kbd>Space</kbd> | Zero-width non-joiner, ZWNJ (`U+200C`) |
| <kbd>Right Alt</kbd> + <kbd>Space</kbd> | Non-breaking space |
| <kbd>Shift</kbd> + <kbd>Right Alt</kbd> + <kbd>Space</kbd> | Narrow non-breaking space |

The Windows shortcut <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>2</kbd> is not implemented by this layout.

## Manual Installation

Use manual installation if you want to review or apply the changes yourself.

1. Clone the repository:

```bash
git clone https://github.com/sinadarvi/windows-persian-keyboard-for-linux.git
cd windows-persian-keyboard-for-linux
```

2. Back up the Persian symbols file and append `ir_patch`:

```bash
sudo cp /usr/share/X11/xkb/symbols/ir /usr/share/X11/xkb/symbols/ir.backup
cat ./ir_patch | sudo tee -a /usr/share/X11/xkb/symbols/ir >/dev/null
```

3. Back up and edit the XKB layout registry:

```bash
sudo cp /usr/share/X11/xkb/rules/evdev.xml /usr/share/X11/xkb/rules/evdev.xml.backup
sudo vim /usr/share/X11/xkb/rules/evdev.xml
```

4. Find the Persian layout and add this variant to its `variantList`:

```xml
<variant>
  <configItem>
    <name>pes_winkeys</name>
    <description>Persian (Windows)</description>
  </configItem>
</variant>
```

5. Open your keyboard settings and add:

```text
Persian (Windows)
```

If the layout does not appear immediately, log out and back in, restart your desktop session, or reboot.

## License

This project is released under the [MIT License](LICENSE.md).
