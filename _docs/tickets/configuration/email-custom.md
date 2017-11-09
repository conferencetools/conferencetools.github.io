---
title: Email Customisation 
permalink: /docs/tickets/configuration/email/
---

To customise the email subject and from addresses for purchase receipts you can use 
the `mailconf` configuration key in the `mail.local.php.dist` file. Each email sent 
by the app has it's own subkey in this array. The following keys are valid:

- `purchase` For the email sent out when a purchase is completed

You can use the following sub keys in each array to configure the email properties

## Subject

Set the `subject` key to customise the subject for the email. Every email will have it's own default
which is used if this key is missed.

## From

Set the `from` key to set the email address emails are sent from. It is highly recommended that you set
this key to help the email be recognised by spam filters as legitimate email.