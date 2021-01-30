# linux-switch-window
Script for window management in Linux

## How to use

1. Copy the file to your system

1.1 My location is `$HOME/bin/switch-window`

1.2 Make if visible to the system `PATH`
```
export PATH=$HOME/bin:/usr/local/bin:$PATH
```
1.3 Make it executable
```
chmod +x export HOME/bin/switch-window
```
2. Install dependencies
```
sudo apt install xdotool
sudo apt install wmctrl
```
3. Check the command works
First argument: app to search \
Second argument: cli to run when the app is not yet open \
Testing with the terminal app
```
switch-window "terminal" "gnome-terminal"
```
4. Assign Keyboard shortcut to it
Setting > Keyboard Shortcuts \
Mine is listed below

| Binding | Action                  |
|---------|-------------------------|
| Super+x | Open/Switch to Terminal |
| Super+b | Open/Switch to Dbeaver  |
| Super+c | Open/Switch to Chrome   |
| Super+e | Switch to Devtools      |
| Super+z | Switch/Cycle VSCode     |

## Special case
There are two special case for me
1. Switch to Devtools but not open it if it's not yet opened
I workaround by let it run `echo` when app is not found
```
switch-window "DevTools" "echo"
```
2. I don't want to open VSCode if it is not yet opened and I want to cycle through VSCode
```
xdotool search --name 'Visual Studio Code' windowActivate %1
```

## References:

```
xdotool search --name " - Google Chrome" windowActivate %1
```
See the window name
```
xdotool getActiveWindow getWindowName
xdotool search --name " - Google Chrome" getWindowName
```
It's better to use `wmctrl` to capture single app because `xdotool` also captures widget window and other window
```
wmctrl -l | grep -i chrome
// See all info here
xwininfo -root -children | grep -i chrome
```
