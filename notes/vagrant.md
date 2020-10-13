### Login to shell

```bash
vagrant ssh
```

### Start Vagrant

```bash
vagrant up
```

### Stop Vagrant and clear data

```bash
vagrant destroy
```

### Stop Vagrant but leave data

```bash
vagrant halt
```

### Connect to MySQL in Vagrant with Sequel Pro

```
SSH host: 127.0.0.1
SSH user: vagrant
SSH key: ~/.vagrant.d/insecureprivatekey
SSH port: 2222

default user/password: vagrant
```

### [windows] Disable time synchronisation

```bash
# disable machine first (vagrant halt)
C:\Program Files\Oracle\VirtualBox\VBoxManage setextradata "%VM_NAME%" "VBoxInternal/Devices/VMMDev/0/Config/GetHostTimeDisabled" 1
# vagrant up
```
