Created by: Drew McLellan
Created date: 2012-05-31
Last updated: 2014-03-12
Authors: Drew McLellan
Title: How can I keep track of traffic with Google Analytics?
Tags: google analytics

# How can I keep track of traffic with Google Analytics?

## Google Analytics is a useful and powerful tool to help you keep track of activity on your website. Here's how you integrate the tracking code into Perch.

Adding Google Analytics code to your a site is straightforward.

## Creating a region

First, add a new region to one of your pages (perhaps the home page) right before the closing `</body>` tag.

	<?php perch_content('Analytics'); ?>

Reload the page in your browser, and the Analytics region should show up as new inside Perch. Click through on the new region and pick the Google Analytics template.

## Add your web property ID

In the edit form, and the “web property ID” that Google gives you to use with your site. It should be in the format `UA-XXXXX-X`.

Save the changes.

## Sharing the region

In the Region Options, check “Share across all pages”, and save.

## Adding the region to other pages

Now copy the Analytics region to the bottom of any existing pages, and add it to any Master Pages you’re using.

	<?php perch_content('Analytics'); ?>

Your Google Analytics code should now show up at the bottom of all your pages, and any new pages you create.