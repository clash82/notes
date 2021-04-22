### Encode file

```bash
gpg --encrypt --sign --armor -r %email% %input file%
```

### Decode file

```bash
gpg --decrypt %input file% > %output file%
```

### List all imported keys

```bash
gpg --list-keys
```

### Import public key

```bash
gpg --import %file%
```

### Increase key trust

```bash
gpg --edit-key %email%

gpg> trust
gpg> quit
```
