Created by: Rachel Andrew
Created date: 2014-11-21
Last updated: 2014-11-21
Authors: Rachel Andrew
Title: A2 Hosting and Perch
Tags: hosting, databases, mysql

# A2 Hosting and Perch

## Support material for setting up your A2 Hosting account to work with Perch.

Perch has partnered with A2 Hosting in order to be able to recommend shared hosting that has good functionality and where we can give specific support material in terms of how to best set up your shared hosting account for Perch.

## Buying your new hosting

We would recommend that you take the Prime + SSD package because an SSD disk in the server your account is on will make a huge difference in the speed of your site.

When registering you’ll be asked if you have an existing domain or want to register a new one. If you want to build a new site and then point the domain later choose a free A2 Hosting subdomain - you can use this as a preview of the site then move the real domain when you are ready.

You can choose to have your site hosted on a server in the USA or Europe (actually Iceland). Choose the location nearest to where the majority of your traffic will come from for the best speeds.

[Sign up with A2 Hosting](http://a2hosting.com/perch-hosting)

### Hosting Options

* I would like to register a domain
* I already have a domain
* Use a free subdomain from A2 Hosting

Unless you are going to move your domain immediately or want to buy a new domain, choose the third option. This will give you a subdomain to preview your site. You can move your domain later.

Under configurable options on the next page you can choose whether to have a server in the USA or Europe, SSD or standard storage.

Pick the location nearest to you. We would advise paying the little extra for an SSD as it will improve the speed of your website.

You do not want any applications auto-installed if you are intending to use Perch!

## Setting up your new hosting account

Once you have your new hosting account there are a few things we would advise that you do.

A2 Hosting accounts come with cPanel and give a large number of options. What we advise you do before installing Perch is make sure you are running the latest version of PHP, and configuring your server to allow reasonably large files to be uploaded via Perch admin.

To get started log into cPanel. You can access cPanel via your account on A2 Hosting, find your list of servers and click Manage then Log into cPanel.

### Selecting a PHP version

In cPanel scroll down to Software/Services and click PHP Version.

Change this to the newest version in the list. At the time of writing that was PHP 5.5.13.

Due to the way cPanel is set up you need to do a couple of things now to configure your server to get the best out of it.

Log into your server with your FTP client (we would suggest using sFTP not regular FTP) and edit the .htaccess file to add the line:

    SuPHP_ConfigPath /home/MYHOME/public_html/

Replace MYHOME with your home directory name - you can see this path in the sidebar under Stats in cPanel.

You then need to create a custom `php.ini` file. You can [download an up to date php.ini from GitHub](https://github.com/php/php-src/blob/master/php.ini-production) or if you know how to do this yourself use your own. [The documentation for A2 Hosting is here](https://www.a2hosting.com/kb/developer-corner/php/custom-php.ini-files).

In the php.ini search for `upload_max_filesize` and set it to something larger enough for the files you might upload. For example 20M. Then search for `post_max_size` and adjust this to a size slightly larger than the one for max_uploads - perhaps 21M.

Put this file inside public_html named php.ini.

This upside of this process is that you have a lot of ability to tweak the PHP configuration by using a PHP.ini file which you may find useful in the future. One of the reasons we are happy to recommend A2 Hosting is that they give you the ability to customise these settings.

## Creating a database

With pre-flight checks done you should now create a database via cPanel. To do this find the Databases section in cPanel and click MySQL Databases.

Under ‘Create New Database’ enter the name of your database. It will automatically be prefixed with your account name. If your account name is ‘birdy’ and you create a database called ‘perch’ then the actual database name is ‘birdy_perch’.

To connect to the database you also need a user. Add your first user under MySQL Users.

Once again usernames will be prefixed with your account name. If you create a user called ‘web’ for your ‘birdy’ account, the actual username is ‘birdy_web’.

The final step is to add this user to the database. Under ‘Add User to Database select your new user and your new database, and click Add. On the next screen give the user All Privileges and click Make Changes.

## Installing Perch

You can now run the Perch Compatibility Test or install Perch using your new hosting. When completing the database details section of the form you enter the database name, the user you just created and their password. Don’t forget the prefixes on the database name and username!

In our tests Perch installed perfectly on A2 Hosting. Once installed take a look at your Diagnostics Report under Settings and you should be able to see that Perch is reporting the correct PHP version and upload size.

## Setting up Perch Scheduled Tasks

After installing Perch you might want to set up [Scheduled Tasks](http://docs.grabaperch.com/docs/scheduled-tasks/), that way any Perch functionality that uses Scheduled Tasks can run.

On Unix hosting this is described as a “cron job” and A2 Hosting have information in the docs about Using [cPanel for cron Jobs](http://www.a2hosting.com/kb/cpanel/advanced-features/cron-jobs).

In your Perch Config you need to define a secret as explained in our [documentation](http://docs.grabaperch.com/docs/scheduled-tasks/). Make sure you reupload your config to the server after adding this.

In the Perch Admin go to Settings > Scheduled Tasks and there should be a line starting with php then the path to the script on your server, ending with the secret you just set. Copy this line.

In cPanel scroll down to the bottom of the page and click Cron Jobs, under Advanced.

Select how often you want the script to run. Once an hour is probably fine unless you need something on your site to update more frequently - you can always update this later.

Then paste the line from Perch into the box labelled Command and click ‘Add New Cron Job’. If you would like to get an email every time it runs you can add your email address in the first box - you might want to do this just to confirm it works then you can remove it.

## Finding Your PHP Error Log

If you are experiencing a “white screen of death” or your page seems to be terminating in a strange way then PHP is probably throwing an error.

You can use the PHP.ini file to choose a location for your PHP error log. I would suggest that you set this up so that it logs into your home directory (not the site root) as then you can view and download it via FTP but it isn’t accessible from a web browser.

The support information from A2 Hosting is [here](http://www.a2hosting.com/kb/developer-corner/php/using-php.ini-directives/php-error-log), but if you search in the php.ini you used earlier for `error_log` you can set it to `/home/YOURACCOUNTNAME/php_errors.log` and you should find that any errors now appear here.
