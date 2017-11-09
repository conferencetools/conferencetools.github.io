---
title: Setup 
permalink: /docs/tickets/configuration/setup
---

Each of the following configuration files must be completed with the correct settings 
in order for the application to function correctly.

## Database

To configure the database make a copy of `doctrine.local.php.dist` as 
`doctrine.local.php` If you are using the provided docker environment, you 
don't need to modify this file, the settings will be populated automatically for you. For a 
production setup, you will need to provide the appropriate settings.
 
## Stripe

To collect payments you will need to enter stripe details. For development ensure you use the 
test credentials provided by stripe. Make a copy of `zfr_stripe.local.php.dist`
as `zfr_stripe.local.php` and enter your secret and publishable keys.

## Email

To configure the database make a copy of `mail.local.php.dist` as 
`mail.local.php` Configure your SMTP settings under the mail array key, the
details under the website key are used to ensure that the correct urls are put in emails 
sent out by the app. 