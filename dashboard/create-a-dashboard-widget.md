Created by: Rachel Andrew
Created date: 2014-03-11
Last updated: 2014-03-11
Authors: Rachel Andrew
Title: How do I create a Dashboard Widget?
Tags: dashboard, control panel

# How do I create a Dashboard Widget?

## Dashboard Widgets display on the home screen of the admin area if you have enabled the Dashboard rather than the traditional listing of pages initial view. Widgets can be created as part of an app, as with our official Perch Apps. However you can also create a standalone widget, that can contain anything from some simple HTML to more complex PHP. This solution shows you how to enable a very simple Widget of your own.

Dashboard Widgets display on the home screen of the admin area if you have enabled the Dashboard rather than the traditional listing of pages initial view.

Widgets can be created as part of an app, as with our official Perch Apps. However you can also create a standalone widget, that can contain anything from some simple HTML to more complex PHP. This solution shows you how to enable a very simple Widget of your own. All this Widget will do is output some HTML, and I’m going to use it to display my upcoming conferences by dropping in my Lanyrd JavaScript badge.

You should be running Perch version 2.0.8 or newer to follow this tutorial.

## Create the files

Dashboard Widgets are really a Perch app. So you will need to create a folder in `perch/addons/apps` to store your widget. I would suggest following the naming conventions used for apps, which is `prefix_appname`. Our official apps are all `perch_appname`. This one is just for me so I’ll name it `rachel_lanyrd`.

Inside your folder you need two files. If you [download the files for this tutorial](../f/download/creat-a-dashboard-widget.zip) you will see that I have created two starting point files for you. These are the minimum requirements for creating a Dashboard Widget and should be placed inside your folder.

* dashboard.php
* admin.php

### dashboard.php

This file contains the minimum mark-up required to enable an app. You should maintain this HTML as it ensures your Widget will work with the others on the Dashboard.

Update the string “Title of your Widget” to whatever title you would like to display at the top of your panel on the Dashboard.

    <div class="widget">
      <h2>
      <?php echo $Lang->get('Title of your widget'); ?>
      </h2>
      <div class="bd">
	      <p>Your content goes here.</p>	
      </div>
    </div>

### admin.php

This file registers an app, it tells the Perch admin that a new app is present. You need this even if your app is just a Dashboard Widget. The first function registers the app with Perch and the second sets which version of Perch you need to be running to use this app.

    <?php
    if ($CurrentUser->logged_in()) {
      $this->register_app('prefix_appname', 'App name', 1, 'App description', '1', false);
      $this->require_version('prefix_appname', '2.0.8');
    }
    ?>

You should update the parameters in the sample file to be correct for your Widget.

* Your app ID (same as the folder your app is in)
* A name/label for your app
* The priority in which is should appear on the Perch tab bar
* A brief description
* A version number
* Should the app show up in the admin menu – set to false for Widget only apps

I have updated mine to look like the following:

    <?php
    if ($CurrentUser->logged_in()) {
      $this->register_app('rachel_lanyrd', 'Lanyrd Conferences', 1, 'Panel to display my conferences', '1', false);
      $this->require_version('rachel_lanyrd', '2.0.8');
    }
    ?>

Simply adding these two files to your folder and refreshing the Dashboard in Perch should make the new Widget show up – it just doesn’t have any content yet.

I can now add some content. In this case all I am going to do is add the two lines of code that will display my Lanyrd badge. So my completed dashboard.php ends up looking like this:

    <div class="widget">
      <h2>
      <?php echo $Lang->get('My conferences'); ?>
      </h2>
      <div class="bd">
	<div class="lanyrd-target-splat"><a href="http://lanyrd.com/profile/rachelandrew/" 
		class="lanyrd-splat lanyrd-type-speaking lanyrd-context-future" rel="me">
        See my conferences on Lanyrd</a></div>
	      <script src="http://cdn.lanyrd.net/badges/person-v1.min.js"></script>	
      </div>
    </div>

This is all you need to do to add a HTML-only Widget to your Dashboard. You could use these to display a message to your users, or include an iframe with content from elsewhere.

By using a little bit of PHP you can easily include other data from a feed or api – see the [official Widgets](http://grabaperch.com/add-ons/dashboard) for some examples.
