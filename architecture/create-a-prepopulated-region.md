Created by: Rachel Andrew
Created date: 2014-03-12
Last updated: 2014-03-12
Authors: Rachel Andrew
Title: Can I create a Region and pre-populate the template used?
Tags: regions, perch_content_create

# Can I create a Region and pre-populate the template used?

## The standard way to create a Perch Region is to use the perch_content PHP tag. You can then select the template used and set up an options in admin. Sometimes you might want to pre-populate a region with a template instead.

Instead of using perch_content, use `perch_content_create()` and pass in an array of options.

    <?php perch_content_create('News', array(
	    'template' => 'article.html',
	    'multiple' => true,
	    'edit-mode' => 'listdetail',
	    'sort' => 'date',
	    'sort-order' => 'DESC',
    )); 
   ?>

Then reload your page in the browser as usual. If the Region does not exist this function will create it. If the Region does already exist perch_content_create will do nothing.

Creating regions in this way is especially useful when you are only going to display the region using perch_content_custom. Create the region **first** with `perch_content_create` and then display it using `perch_content_custom`.

Read the documentation for [perch_content_create](http://docs.grabaperch.com/docs/developers/creating-regions/).