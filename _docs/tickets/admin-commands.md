---
title: Admin Commands
permalink: /docs/tickets/admin-commands/
---

Administration of the application is currently done via a command line interface, to
run the commands you will need to be logged in on the server running the code. These
functions will eventually be made available via an API as well.

### Issue free tickets

This command is intended to allow you to override the frontend requirement for payment
on all tickets and provides a more secure way to issue free tickets to sponsors, speakers
competition winners etc than issuing a 100% discount, discount code. It can also be
used for issuing ticket for which an offline payment has been received (eg a direct
bank transfer)

The command is 
`php vendor/bin/cli tickets:issue-free-ticket [--number=1] [--discountCode=""] <ticket type> <email>`

It has four parameters:

#### TicketType (mandatory)

This parameter is the ticket type to issue, use the config key of the ticket type 
you wish to issue as the parameter value.

We recommend that you create a specific ticket type for issuing free tickets 
via this method and set it to private so that it isn't available to purchase. 
This avoids depleting the remaining stock of purchasable tickets when you issue 
tickets to sponsors, speakers etc. 

#### Email (mandatory)

This parameter is the purchaser email for the ticket, it will be used to send a
purchase receipt to which will include the management URL for the ticket.

#### Number (optional)

The number option defaults to one, but can be specified to issue more than one 
ticket per purchase.

#### Discount Code (optional)

The discount code is another optional paramter, if specified it will apply the 
given discount code to the purchase total. This is useful if you have taken an 
offline payment for an order and you wish to apply a discount to the order. 
Specifying the code will ensure it's present on the receipt and that the price is
calculated correctly. If used it should be set to the config key of the discount
code you wish to apply.
 
### Cancel ticket

The cancel ticket command is used to void an individual ticket, after it has been
voided, the details will no longer appear in any ticket reports and the ticket 
holder will not be able to use the management link to change the ticket details.

You must cancel each ticket in a purchase separately.

This command does not release the ticket back for purchase.

This command does not issue a refund (you must handle this yourself).

The command is 
`php vendor/bin/cli tickets:cancel-ticket <purchase id> <ticket id>`

#### Purchase Id (mandatory)

The purchase id which contains the ticket you wish to cancel. This is the long string
identifier in the management URL.

A purchase record will only be removed if there are no valid tickets still assigned
to it. If you cancel the last ticket, the purchase record will be deleted as well.

All data pertaining to the purchase will be retained in the event log should you 
need to retrieve it (eg to resolve a dispute with a customer)

#### Ticket Id (mandatory)

The ticket Id to cancel. This is the short string on the end of the management URL.

### Report to Csv

The report to csv command produces a csv file of a database report the command is: 

`php vendor/bin/cli tickets:report-to-csv <report name> [output file]`

#### Report name (mandatory)

The report name you wish to generate. The possible values for this parameter
are:

- delegate_information
- delegate_requirements
- missing_delegate_information
- ticket_mailout 
- ticket_sales 
                 
More details on the reports can be found on the <reports> page

#### Output file (optional)

The filename to write the result to. Defaults to /tmp/report.csv if the filename
is not provided

### Timeout purchases

The timeout purchases command is intended to be called on a regular basis by a cron
job. It will remove records pertaining to abandoned purchases eg where a customer has
started the purchase process but hasn't completed payment. This will then release
the tickets for other customers to purchase. Should you need to run this command
manually you can do so with:
`php vendor/bin/cli tickets:timeout-purchases`

### Rebuild projections

The rebuild projections command recreates the read models based off the event log.
This is an advanced command which you should only rarely need to run. Currently the
only projection which supports rebuilding is the ticket counts projection, which 
stores the number of tickets of each type that are remaining. If you make 
certain changes to the ticket config (adding or removing a ticket type, or changing
the number of tickets available), you will need to run this command for the changes
to take effect.

`php vendor/bin/cli cqrs:rebuild-projection -a`