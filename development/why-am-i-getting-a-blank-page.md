Created by: Rachel Andrew
Created date: 2014-03-11
Last updated: 2014-03-11
Authors: Rachel Andrew
Title: Why am I getting a blank page?
Tags: debug

# Why am I getting a blank page?

## The dreaded White Screen of Death means you have a PHP error that is not being output to the screen. This solution explains what to do.

If you try to load a PHP page and get no HTML output at all - the **white screen of death** then PHP is erroring before and output is written. You can check to see if this is the case by Viewing Source. The View Source should be completely empty as well.

If this is happening then you have a PHP Error. The quickest way to solve the problem is to find the error, which will be located in your PHP error log. If you are using MAMP, XAMPP or similar locally then check the documentation to find the location of your error log.

On a live server you may need to ask your host the location of your error log. You can often configure error logging yourself, this [Smashing Magazine article](http://coding.smashingmagazine.com/2011/11/30/a-guide-to-php-error-messages-for-designers/) has information on how to do that.

Once you have access to the log, reload the problematic page and look at the most recent error. The most common reasons for a white screen of death in Perch are as follows.

## Errors relating to missing files

You will either see an error saying something like:

    PHP Warning:  include(perch/runtime.php): failed to open stream: No such file or directory in /home/mysite/public_html/test.php on line 2

Or, you will get errors about undefined functions.

This usually means that the Perch runtime is not included with a correct path or you are trying, for example, to use the Blog app functions but did not include the blog runtime in apps.php.

## Errors relating to permissions

Hosts will require different permissions for PHP files, and for folders where files may be uploaded. If you use the wrong permissions you will see errors that say **Permission Denied**. If you are seeing these errors you need to speak to your host and check the permissions you need to use.

## If all else fails bring your error to support

We'll be very pleased to see a support ticket with an actual error as that is usually something we can help with very quickly. So if you can't figure out why you are getting the error or you do not understand the reply from your host then raise a ticket and we'll get you sorted.
