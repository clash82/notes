### Generate entities based on the existing properties (Sf3)

```bash
php bin/console doctrine:generate:entities AppBundle:%entity%
```

### Update database schema based on the existing entities (Sf3)

```bash
php bin/console doctrine:schema:update --force
```
