---
title: Installation 
permalink: /docs/tickets/
---

### Using the stand along application

1. Download or fork the ticket application repository.
2. Run composer install
3. Copy and amend the example configuration files 
4. Apply any customisations to css, views and images you wish to make
5. Run `php vendor/bin/doctrine-module orm:schema-tool:create` This creates the database schema.
6. Run `php vendor/bin/cli cqrs:rebuild-projection -a` This imports the initial data into the database.


