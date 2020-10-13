### Update WordPress SVN repository standard procedure

This guide includes steps required to update existing plugin in the official WordPress SVN repository.

- checkout the existing SVN repo:

```bash
svn co https://plugins.svn.wordpress.org/%plugin_name% %plugin_local_dir%
```

- copy updated files to the `trunks` directory
- add new files to the repo:

```bash
svn add --force trunk/*
```

- commit trunk:

```bash
svn ci -m "Adding updated files for the v0.1.0 release"
```

- tag a new plugin version:

```bash
svn cp trunk tags/0.1.0
```

- check in the changes:

```bash
svn ci -m "Tagging version 0.1.0"
```
