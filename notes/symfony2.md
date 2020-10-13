### Clear cache in production environment

```bash
php app/console cache:clear -e=prod
```

### Dump assets

```bash
php app/console assetic:dump
```

### Start assets watching

```bash
php app/console assetic:watch
```

### Run built-in PHP server

```bash
php app/console server:run
```

### Dump semantic configuration for specified reference

```bash
php app/console config:dump-reference %reference_name%
```

### Move vendor directory to a different location

This is very useful if you want to speed-up your work with Symfony in Vagrant VM (move `vendor` directory inside your Vagrant Box file structure).

- go to the sf2 project root directory
- remove `vendor` directory
- create `vendor` directory in new location (eg. `/home/vagrant/sf2_vendor`):

```bash
mkdir /home/vagrant/sf2_vendor
```

- symlink new directory:

```bash
ln -s /home/vagrant/sf2_vendor vendor
```

- run `composer install` again
- ignore `vendor` file globally in Git:

```bash
git config --global core.excludesfile '~/.gitignore_global'
vim ~/.gitignore_global
```

- optional: include new `vendor` path in PhpStorm (Settings &raquo; PHP &raquo; inlude path)
