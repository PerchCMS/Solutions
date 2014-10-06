Created by: Rachel Andrew
Created date: 2014-10-06
Last updated: 2014-10-06
Authors: Rachel Andrew
Title: Using Perch with Mailtrap for local email testing
Tags: email, forms

# Using Perch with Mailtrap for local email testing

## During development on a local server testing forms and email can be tricky. This solution explains how to integrate the service Mailtrap with Perch.

[Mailtrap](https://mailtrap.io) is a service that can capture all emails send from your application, allowing you to test form to email scripts and other integrations without needing to set up and configure a local mail server. It’s really easy to use Mailtrap with Perch.

Create your [mailtrap](https://mailtrap.io) account. You can sign up for a free single user account using your GitHub or Google credentials or create an account with an email address and password.

Once you have created your account click on the Inbox that has been created. To integrate Mailtrap with Perch you’ll need the Host, Username and Password listed under SMTP.

Open your Perch config/config.php in a text editor and add the following details, replacing `mailtrap_host`, `mailtrap_username` and `mailtrap_password` with your settings.

    define('PERCH_EMAIL_METHOD', 'smtp');
    define('PERCH_EMAIL_HOST', 'mailtrap_host');
    define('PERCH_EMAIL_SECURE', 'tls');
    define('PERCH_EMAIL_AUTH', true);
    define('PERCH_EMAIL_PORT', 2525);
    define('PERCH_EMAIL_USERNAME', 'mailtrap_username');
    define('PERCH_EMAIL_PASSWORD', 'mailtrap_password');

You can test to see if your integration is working by going to - Settings > Email in Perch and sending the test email. It should be caught by Mailtrap and show up in your inbox.

Now any email that Perch sends will show up in Mailtrap making it easier to test your forms.

When you go live, you will need to remember to change those details for your live mail server details, or just remove them if PHP can send mail from your server without additional configuration. You could also add the details to a block in your config file following this solution for [creating Config Files that work on multiple servers](/development/multiple-server-config).


