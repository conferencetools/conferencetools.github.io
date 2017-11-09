---
title: Google Analytics
permalink: /docs/tickets/configuration/google-analytics/
---

To configure Google Analytics make a copy of `module/GoogleAnalytics/config/google-analytics.local.php` as 
`config/autoload/google-analytics.local.php` and set your own Google Analytics tracking ID.

By default, the tracking ID is an empty key, which disables the Google Analytics integration.

If you override the `layout.phtml` view with your own do no forget to call the view helper
(`<?= $this->googleAnalytics() ?>`) in the `<head>` section.