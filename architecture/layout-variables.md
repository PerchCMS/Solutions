Created by: Rachel Andrew
Created date: 2014-03-12
Last updated: 2014-03-12
Authors: Rachel Andrew
Title: If my page title is in a layout, how do I pass in a unique title?
Tags: layouts, variables

# If my page title is in a layout, how do I pass in a unique title?

## You are using Perch Layouts for your includes but you need to be able to insert the title for each page into that layout include.

[Perch Layouts](http://docs.grabaperch.com/docs/layouts/variables/) can accept variables, these could be hardcoded or be added by your editors. By using Layout Variables you can add unique titles for each page.

In the layout that includes the title element add the following.

    <title><?php perch_layout_var('title'); ?></title>

When add your layout to a page include the title as a variable. The first value `global.header` is just the name of my layout, the second an array including any variables. I just have one here - the title.

    <?php
    perch_layout('global.header', array(
	    'title'=>'Welcome to my site!'
    ));
    ?>

The above is fine if you want to hardcode a title and set it as a variable. You can also pass in the title added when editing the page.

    <?php
    perch_layout('global.header', array(
	    'title'=>perch_pages_title(true),
    ));
    ?>

Or you can get a value from elsewhere - for example the title of your blog post.

    <?php
    $title = perch_blog_post_field(perch_get('s'), 'postTitle', true);
    perch_layout('global.header', array(
	  'title'=>$title
    ));
    ?>
