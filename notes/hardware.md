### Disable built-in hard disk password with data destroy

You can check current HDD state by executing command below:

```bash
sudo hdparm -I /dev/sdX
```

If state is `frozen` then there is no way to clear password other than erasing all data on that disk.

To unfreeze disk you first need to enable suspend mode:

```bash
sudo systemctl suspend
```

Then you have to create a new password (will be overwritten anyway):

```bash
sudo hdparm --security-set-pass NULL /dev/sdX
```
 
And finally we are running erase command on that disk:

```bash
sudo hdparm --security-erase NULL /dev/sdX
```

This operation may take up to several hours, progress is not reported. After that all data will be destroyed and master password will be removed.
