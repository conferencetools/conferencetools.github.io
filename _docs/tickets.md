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
7. Setup a cron job for `php vendor/bin/cli tickets:timeout-purchases` to run frequently
   we advise once per minute, this command releases tickets which have been reserved
   but have not completed payment. 


