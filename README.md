# windows-persian-keyboard-for-ubuntu
How to customize ubuntu persian keyboard layout to be like windows

## steps
 1. first go to xkb folder
```bash
cd /usr/share/X11/xkb/symbols
```
 2. make backup of persian symbol file
```bash
cp ./ir ./ir-backup
```
 3. copy `ir` file below and then modify symbols file
```bash
sudo gedit ./ir
```
 4. make backup of layout declaration
```bash
cd /usr/share/X11/xkb/rules
cp ./evdev.xml ./evdev-backup.xml
```
5. Add the new layout declaration to /usr/share/X11/xkb/rules/evdev.xml (or copy `evdev.xml` file and paste it there)
```bash
sudo gedit ./evdev.xml
```
add this line after `Persian (with Persian keypad)` section
```xml
...
<variant>
  <configItem>
    <name>pes_win</name>
    <description>Persian (Windows layout)</description>
  </configItem>
</variant>
...
```
