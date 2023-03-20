**Note: if you are using xkeyboard-config version 2.39 or newer, you already have the Windows Persian layout installed, and don't need this repo.**

I have been looking for a way to change to the keyboard layout of the Persian language for the Ubuntu operating system for a few years, which might be identical to the one I used to have while I was a windows user. This is probably the problem of most of the people who want to use Ubuntu. However, they cannot switch to it since it is almost impossible to type correctly using its predefined Persian language keyboard.

I hope it would be helpful for those who get used to the layout of Windows and love to work with a real operating system.

Enjoy.


## Automatic Installation

The automatic installer script requires `xmlstarlet` to be installed.
Install it using your package manager before running the script.

**Warning: The automatic installer does not detect any previous versions of this project. If you are updating from a previous version, make sure you don't already have an older version of the Windows Persian layout installed.**

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


## Manual Installation

1. Clone the repository

```bash
git clone https://github.com/sinadarvi/windows-persian-keyboard-for-linux.git
cd windows-persian-keyboard-for-linux
```

2. Append the `ir_patch` file from the repo to the `ir` symbols file.

```bash
sudo cp /usr/share/X11/xkb/symbols/ir /usr/share/X11/xkb/symbols/ir.backup
cat ./ir_patch | sudo tee -a /usr/share/X11/xkb/symbols/ir >/dev/null
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
            <name>winkeys</name>
            <description>Persian (Windows)</description>
          </configItem>
        </variant>
```

4. All done! You can now go to your keyboard settings and add the `Persian (Windows)` layout.
