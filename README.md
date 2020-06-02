
I have been looking for a way to change to the keyboard layout of the Persian language for the Ubuntu operating system for a few years, which might be identical to the one I used to have while I was a windows user. This is probably the problem of most of the people who want to use Ubuntu. However, they cannot switch to it since it is almost impossible to type correctly using its predefined Persian language keyboard.  Finally, this nightmare ended for me when I find what dear @KotlinFarsi did a few years ago. However, after following his instruction, I realized that this is not working at least on version 18.04 LTS+. So I decided to read his codes and generate an updated version of his file, which would work correctly. Here is the upgraded version of the file that I am currently using on Ubuntu 20.04 LTS.

The instruction is the same. I replaced the `ir` file with the updated version. I hope it would be helpful for those who get used to the layout of windows and love to work with a real operating system.

Enjoy.

# Windows persian keyboard for ubuntu
How to customize ubuntu persian keyboard layout to be like windows


# Step

You have two options, either do it manually or use CURL to install it.

## Automatic installation :
1. You need to run the following command and the scrip will perform the steps for you.

```bash
 curl -s -L https://raw.githubusercontent.com/rez4mt/windows-persian-keyboard-for-ubuntu/master/install | sudo bash -
```
2. now logout and when you log back, go to `settings > Region and language` (or where ever your keyboard perference is) and in input sources click on `+` button and search for `Persian (Windows layout)`, and add it.

## Manual :
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
6. now logout and when you log back, go to `settings > Region and language` (or where ever your keyboard perference is) and in input sources click on `+` button and search for `Persian (Windows layout)`, and add it.


