Created by: Rachel Andrew
Created date: 2014-03-11
Last updated: 2014-03-11
Authors: Rachel Andrew
Title: How do I debug problems with templates or custom content?
Tags: debug

# How do I debug problems with templates or custom content?

## Perch has a debug mode that can help you see what Perch is doing internally. This is helpful for troubleshooting your own problems and will give you extra information to give to support when you need help.

To switch on debug add the following line to your `perch/config/config.php` file.

    define('PERCH_DEBUG', true);

This will output debug underneath your admin area. If you also want to show debug at the bottom of pages on your site, add the line above and then add the following to any page where you want to see debug (or into a global footer layout or include).

    <?php PerchUtil::output_debug(); ?>

This will only output if you have turned on `PERCH_DEBUG` in your configuration file.

## What can debug show you?

On the front-end of your site debug will show you the SQL queries that run when a page is loaded. You will be able to see if an SQL error is being thrown - which would explain missing content.

Debug will also show you the template that is being used. It should then be very obvious if - for example - you think Perch should be using a custom template but is instead using one of the defaults due to a typo.

On apps such as Blog that cache certain parts of the page - such as the category listing you can see if the content came from the cache.

Having debug turned on during development can save a lot of frustration and help you get support more quickly.




