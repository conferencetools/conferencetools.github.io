---
title: Advanced Customisation
permalink: /docs/tickets/configuration/advanced/
---

The application is based on Zend Framework and is very flexible and most of it can 
be overridden and changed in the same manner which you would for any Zend 
application, this section contains some examples of the more common things which 
you might want to change. All of the changes in these sections require you to add
an additional config file to the `config/autoload` directory of the main application.
This file should return an array of config to be merged with the application config
eg:

```php

return [
    'custom_config_key' => 'custom_config_value'
];

```

Refer to the module config in the tickets module for all the config key values you
can change. Bear in mind that some changes may break the application and that we can
only offer limited support for these advanced changes.

### Overriding views

@TODO

### Overriding routes

You can change the base uri for the app with the following piece of config.

`'router' => ['routes' => ['tickets' => ['options' => ['route' => '/tickets/' ] ] ] ]`

This example would prefix all application urls with `/tickets/`

### Overriding assets

To override individual assets, add a `map` key to the asset manager eg

`'asset_manager' => ['resolver_configs' => ['map' => ['css/card.css' => 'my.new.css'] ] ]`

### Additional delegate information

@TODO fill out with more details + code examples

The basic steps to add additional delegate information fields are as follows:

1. Create a Delegator factory (see zend docs) for the delegate information fieldset
2. Inside the delegator factory, call the original service factory to retrieve the fieldset
3. Add your additional fields (see zend form docs)
4. Return the modified fieldset
5. Add delegator factory to config

! Functionality hasn't been merged yet ! 

### Validating delegate information

@TODO Add more details

You can add validation to the delegate information (eg make specific fields required)
however bear in mind the same configuration is used for both the initial purchase and
for the management page, so ensure that you test both places if you change the validation

Override the config using the key:

```php
'input_filter_specs' => [
    \ConferenceTools\Tickets\Form\ManageTicket::class => ['your config here'],
],
```
     
The current configuration is located in the file 
`config/input-filters/manage-ticket.config.php`