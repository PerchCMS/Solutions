Created by: Rachel Andrew
Created date: 2014-03-11
Last updated: 2014-03-11
Authors: Rachel Andrew
Title: How do I allow users to change a class applied to the body element of a page?
Tags: CSS

# How do I allow users to change a class applied to the body element of a page?

## It is sometimes useful to have functionality where editors can change a class on the body element. This can facilitate choosing the colour scheme for a page, or allowing you to set a background image based on that selection. You can do this using Page Attributes.

To add a class to the body element I create a new template in `perch/pages/templates/attributes` and name it `body_attributes.html` this template includes a select list of classes.

    <perch:pages id="bodyclass" label="Page Theme" 
help="Select the theme for this page" type="select" 
options="red,green,blue" />

You can use all of the usual Perch Template tags and attributes in Page Attributes.

I then include this template in the template `pages/attributes/default.html`.

    <perch:template path="pages/attributes/body_attributes.html" /> 

On my page, I add this to the body element using the perch_page_attribute function – this just returns a single attribute from the template. 

    <body class="<?php
    perch_page_attribute('bodyclass', array(
        'template' => 'body_attributes.html'
    ));
    ?>”>

You can see this process in our [Page Attributes video](http://docs.grabaperch.com/video/tutorials/techniques/page-attributes/). Also read the [Page Attributes documentation](http://docs.grabaperch.com/docs/pages/page-attributes/) to learn more about the feature.