# How do I move a Perch site?

## If you need to move a site from development to live or from one live server to another, follow these steps.

In a previous article I explained how to set up a local development environment using XAMPP so that you can work locally on your Perch sites. Once you have built your site you will need to move it to a live or staging server and this article explains how to do that.

These instructions are also to be followed if you are moving your site from staging to live, or moving your site between two live servers if you are changing hosts. I will refer throughout this tutorial to Old Server and New Server. Old Server is where the site is currently, New Server is where you are moving it to.

To move your Perch site and all of the content you will need to do the following things:

1. Run the Perch Server Compatibility Test on the new server
2. Take a copy of your database and transfer it to the new server
3. Update your config file so that the connection details are correct for the new server
4. Upload all of your files – including the perch folder to the root directory of the new server

## Step 1: Run the Perch Server Compatibility Test on the new server

This step makes sure that the new server can run Perch and also checks your database connection details so that you have no problems when setting up the site.

You will need to know your:

* database server location (it may be localhost or your host may have given you a server URL or IP address)
* the name of the database
* your database username and password

Download the test, upload it to the server and run it. We have a [video](http://docs.grabaperch.com/video/compatibility-test/) detailing all of the possible errors and what they mean. If you need to contact your host to check database details then this is the time to do it – before you have started to deploy your site!

## Step 2: make a copy of your database and transfer it to the new server

I am assuming here that you have phpMyAdmin running locally as described in the tutorial about setting up XAMPP and that your host also has phpMyAdmin. It is likely that this will be accessed via your hosting control panel under databases.

## On the old server

Open phpMyAdmin locally. In XAMPP go to http://localhost click phpMyAdmin in the sidebar and log in.

Select your website database in the sidebar. Then Click Export in the navigation.

### Exporting the database	

The defaults of **SQL** and to **download a file** should be all you need. Click Go and save the file to your computer.

This text file contains all of the information that MySQL needs to fully recreate your database and all of your content on a new server.

### On the new server

Log into phpMyAdmin using the details provided by your host and select the database you are going to use for Perch. This should be the database that gave you a pass when using the Server Compatibility Test.

Select Import from the Navigation.

Browse for the file that you just saved from the old server. Set the Character Set to `utf-8`. The other options should be fine to leave as default.
Import data	

Hit Go and your database will import, after import you should be able to see all of the tables appear in the sidebar in phpMyAdmin.

## Step 3. Update your config file so that the connection details are correct for the new server

If you are moving your files from the root of your development site to the root of your live site as suggested then the only file you need to change is your Perch Config file, as it will currently have the database settings for the old server.

You probably want to keep your development version working so in a text editor copy the following lines:

    define("PERCH_DB_USERNAME", 'root');
    define("PERCH_DB_PASSWORD", 'xxxxxx');
    define("PERCH_DB_SERVER", "localhost");
    define("PERCH_DB_DATABASE", "db-site1");

Paste them in the config file below the original lines so they are now listed twice. Change the details in the second set so that you use the MySQL server, database name, username and password for the new server. Then comment out your local ones for now. You can then change it back to keep working on the local server.

You could also follow the instructions give in our guide to creating a multiple server config file for Perch.

    /* define("PERCH_DB_USERNAME", 'root');
    define("PERCH_DB_PASSWORD", 'xxxxxx');
    define("PERCH_DB_SERVER", "localhost");
    define("PERCH_DB_DATABASE", "db-site1"); */

    define("PERCH_DB_USERNAME", 'mysite_username');
    define("PERCH_DB_PASSWORD", 'xxxxxx');
    define("PERCH_DB_SERVER", "localhost");
    define("PERCH_DB_DATABASE", "mysite_databasename");

## Step 4: Upload all of your files

With your config file edited all you need to do is upload all of your site files – including the Perch folder – from your old to the new server. All of your content should then be in place and your site is live on the new server.

If you are moving servers rather than transferring your local copy, remember that you need to move all of the contents of the resources folder as this is where any images and files that your client has uploaded will be.

Remember that you will need to make the resources folder writable on the new server – just as when you first installed Perch – so that file uploads can be placed there.