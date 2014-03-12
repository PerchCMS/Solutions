Created by: Rachel Andrew
Created date: 2014-03-12
Last updated: 2014-03-12
Authors: Rachel Andrew
Title: Can I combine content from several regions?
Tags: perch_content_custom

# Can I combine content from several regions?

## You want to gather content from more than one Perch Region, and display it on a page.

The first argument to [perch_content_custom](http://docs.grabaperch.com/docs/content/perch-content-custom/) is the key (or name) of the region you want to fetch the content from. However it can also be an array of keys.

You can also get content from more than one page by passing an array of page URLs as the value of page in the second argument.

If you have more than one place that content is being added but then want to combine it, this can be very useful. The following example combines data from two regions on two different pages. I have been careful to use the same IDs in each template for the content so I can output it all using a single template.

    <?php perch_content_custom(array('Writing','Podcasts'), array(
      'count'=>10,
		  'template'=>'_external_resource.html',
		  'page'=>array('/writing/index.php','/podcasts/index.php'),
		  'sort'=>'date',
      'sort-order'=>'RAND'
    )); 
		?>