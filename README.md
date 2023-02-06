
I have been looking for a way to change to the keyboard layout of the Persian language for the Ubuntu operating system for a few years, which might be identical to the one I used to have while I was a windows user. This is probably the problem of most of the people who want to use Ubuntu. However, they cannot switch to it since it is almost impossible to type correctly using its predefined Persian language keyboard.  Finally, this nightmare ended for me when I find what dear @KotlinFarsi did a few years ago. However, after following his instruction, I realized that this is not working at least on version 18.04 LTS+. So I decided to read his codes and generate an updated version of his file, which would work correctly.

The instruction is the same. you should add `ir_win` file and change some settings. I hope it would be helpful for those who get used to the layout of windows and love to work with a real operating system.

Enjoy.

# installation :
1. You need to run the following command and the scrip will perform the steps for you.

```bash
 curl -s -L https://raw.githubusercontent.com/sinadarvi/windows-persian-keyboard-for-ubuntu/master/install | sudo bash -
```
2. now go to `settings > Keyboard` (or where ever your keyboard perference is) and in input sources click on `+` button and search for `Persian (Windows layout)`, and add it.



