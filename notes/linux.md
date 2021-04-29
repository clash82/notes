### [tmux] attach to existing sessions

```bash
tmux attach
```

### [tmux] keyboard shortcuts

```bash
Ctrl+B + C = new session
Ctrl+B + N = next session
Ctrl+B + W = session list
Ctrl-B + 1..9 = switch to specified session
Ctrl-D = kill current session
Ctrl+B + Shift+5 = split screen
Ctrl+B + Left/Right = move between screens
```

### [python] run dummy SMTP server for development purpose

```bash
sudo python -m smtpd -n -c DebuggingServer localhost:25
```

### [bash] clear directory

```bash
rm -rf %path%
```

### [bash] find file

```bash
find %path% -name "%filename%"
```

### [bash] get size of element on disk

```bash
du -hs %path%
```

### [bash] find string in files

```bash
grep -r %string% *
```

### [bash] generate SSH keys and copy to destination machine

```bash
ssh-keygen -t rsa -b 2048
ssh-copy-id %login%@%host%
```

### [bash] create symbolic link

```bash
ln -s %file_path% %link_path%
```

### [bash] compress file with password

```bash
zip -e %archive_name% %file_path%
```

### [bash] show Linux version

```bash
lsb_release -a
```

### [bash] keep showing only important entries from logs

```bash
tail -f var/logs/* | grep -E 'ERROR|CRITICAL'
```

### [ubuntu] enable the `universe` repository

```bash
sudo add-apt-repository universe
```

### [ubuntu] change owner of the partition

```bash
sudo chown %user%:%user% /media/%disk_label% -R
```
