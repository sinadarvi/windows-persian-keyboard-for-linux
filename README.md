I have been looking for a way to change to the keyboard layout of the Persian language for the Ubuntu operating system for a few years, which might be identical to the one I used to have while I was a windows user. This is probably the problem of most of the people who want to use Ubuntu. However, they cannot switch to it since it is almost impossible to type correctly using its predefined Persian language keyboard.

The instruction is the same. you should modify the `ir` and `evdev.xml` files. I hope it would be helpful for those who get used to the layout of windows and love to work with a real operating system.

Enjoy.

**Note: If your Linux distribution has a version of xkb with [!473](https://gitlab.freedesktop.org/xkeyboard-config/xkeyboard-config/-/merge_requests/473) merged, you already have a Windows Persian layout, and do not need this repo.**


## Automatic Installation

The automatic installer script requires `xmlstarlet` to be installed.
Install it using your package manager before running the script.

**Warning: The automatic installer does not detect any previous versions of this project. Make sure you don't already have an older version of the Windows Persian layout installed.**

1. Clone the repository

```bash
git clone https://github.com/sinadarvi/windows-persian-keyboard-for-linux.git
cd windows-persian-keyboard-for-linux
```

2. Run the installer script as root

```bash
sudo ./install
```

3. All done! You can now go to your keyboard settings and add the `Persian (Windows)` layout.


## Enable From the Terminal

After installing the layout, you can enable it for the current X11 session with:

```bash
setxkbmap -layout us,ir -variant ',pes_winkeys' -option grp:alt_shift_toggle
```

This configures `us` and `ir` layouts, uses the `pes_winkeys` variant for the Persian layout, and enables switching between layouts with <kbd>Alt</kbd> + <kbd>Shift</kbd>. The leading comma in `',pes_winkeys'` means that no variant is set for the first layout (`us`).

To make this persistent, add the command to your X session startup file, such as `~/.xprofile`, `~/.xinitrc`, or your desktop environment/window manager autostart configuration. Avoid adding it to `~/.bashrc`, because that file runs for every interactive shell and may run when no X11 session is available.


## Manual Installation

1. Clone the repository

```bash
git clone https://github.com/sinadarvi/windows-persian-keyboard-for-linux.git
cd windows-persian-keyboard-for-linux
```

2. Append the `ir_patch` file from the repo to the `ir` symbols file.

```bash
sudo cp /usr/share/X11/xkb/symbols/ir /usr/share/X11/xkb/symbols/ir.backup
sudo cat ./ir_patch | sudo tee -a /usr/share/X11/xkb/symbols/ir &>/dev/null
```

3. Edit the xkb layouts registry with your text editor of choice (vim for example),

```bash
sudo cp /usr/share/X11/xkb/rules/evdev.xml /usr/share/X11/xkb/rules/evdev.xml.backup
sudo vim /usr/share/X11/xkb/rules/evdev.xml
```

find the Persian layout and add this variant to the list of variants for Persian:

```xml
        <variant>
          <configItem>
            <name>pes_winkeys</name>
            <description>Persian (Windows)</description>
          </configItem>
        </variant>
```

4. All done! You can now go to your keyboard settings and add the `Persian (Windows)` layout.
