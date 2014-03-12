Created by: Rachel Andrew
Created date: 2014-03-12
Last updated: 2014-03-12
Authors: Rachel Andrew
Title: How do I let my editor choose pages for a footer or header navigation bar?
Tags: navigation, navigation groups

# How do I let my editor choose pages for a footer or header navigation bar?

## You have a few quick links to important pages - for example contact, find us and site map and want to let you editor choose which links appear there.

[Navigation Groups](http://docs.grabaperch.com/docs/navigation/navigation-groups/) were designed to solve this problem.

Log into Perch Admin and create a Group by visiting Pages > Navigation Groups.

You group then displays in the Page Options for each page, and pages can be added or removed.

On you page - or in your Perch Layout - you can then include the group by calling perch_pages_navigation using the group slug.

    <?php perch_pages_navigation(array(
      'navgroup' =>'footer',
      'levels' => 1
    )); ?>