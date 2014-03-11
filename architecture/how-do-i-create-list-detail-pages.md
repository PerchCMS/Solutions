# How do I create list and detail pages in Perch?

## A common pattern in many websites is the idea of list-and-detail pages. One view shows a list of items, and clicking through shows more detail about the chosen item. This can be accomplished with Perch using a multiple-item content region.

This guide will show you how to set up list and detail pages for a simple list of products. The same technique would apply for many other types of content, such as news articles, real estate listings, events and so on.

If you get lost, you can download the example files from the end of the article and get back on track.

## Setting up the templates

We need two templates – one for the detail view (showing all the information) and one shortened view for the listing page.

### Detail template

The detail template is the master template – the one that’s used for editing. It needs to include fields for all the information you want to appear in the edit form. It is used for the detail page when the user clicks through from a listing.

In our case, it needs to represent one single product. Save this as product_detail.html

    <h1><perch:content id="title" type="text" label="Product title" required="true" title="true" /></h1>
    <perch:content id="image" type="image" label="Image" width="640" output="tag" />
    <perch:content id="desc" type="textarea" label="Description" textile="true" editor="markitup" />
    <p>Price: &pound;<perch:content id="price" type="text" label="Price" format="#:2" /></p>
    <perch:content id="slug" for="title" type="slug" suppress="true" />
    <perch:content id="image" type="image" label="Image" width="100" height="100" crop="true" suppress="true" />

At the end of the template we’ve added an additional size for the image – the suppress="true" attribute will stop it being output on the detail template, but keeps it available for us to use on the listing template. As this is the master template, all the image sizes we want to use need to be defined here, else they won’t be created.

We’ve also added a ‘slug’ field. This makes a URL-friendly version of the title for use when linking to the detail page. It is also suppressed, as we don’t want to show it here, just make sure it’s created.

### List template

The list template is just a simplified version of the detail template. The only addition is before and after sections, to add the right markup for a list. Save this as product_listing.html

    <perch:before>
    <ul>
    </perch:before>
    <li>
     <a href="?s=<perch:content id="slug" type="slug" />">
          <perch:content id="image" type="image" width="100" height="100" crop="true" output="tag" />
          <perch:content id="title" type="text" />
     </a>
    </li>
    <perch:after>
    </ul>
    </perch:after>

As well as adding markup to make this a list of items (the `<ul>` and `<li>` tags) we’ve added a link. The link uses the slug field as a query string parameter. That means that if our listing page URL looks like:

`/products.php`

a detail page might look like:

`/products.php?s=wooden-handled-claw-hammer`

You can, of course, use mod_rewrite rules to write cleaner URLs, but we’ll keep this simple for now.

## Setting up the page

Now that we have our templates, it’s time to create the page. We’re going to use one page that acts in a different way depending if it’s in list or detail mode.

_Tip: You can use two different pages if you prefer, by splitting the parts out. Perhaps follow along with this one-page example first, until you understand how it’s working._

Create a new page, products.php, with whatever boilerplate code you’d like to use for the page. Here’s mine:

    <?php include('perch/runtime.php'); ?>
    <!doctype html>
    <html lang="en">
      <head>
        <meta charset="utf-8" />
        <title>Products</title>
      </head>
      <body>

      </body>
    </html>

## Creating the region

Normally, new regions are created by putting a `perch_content()` region in the page. In this instance, we’ll be displaying the content using `perch_content_custom()` for both the list and the detail view. Therefore, we’ll use `perch_content_create()` to set up the region instead.

    <?php
    perch_content_create('Products', array(
     'template'   => 'product_detail.html',
     'multiple'    => true,
     'edit-mode' => 'listdetail',
    ));
    ?>

Here we’re specifying the detail template as the master template for the region. We’re setting multiple to true, so that the region allows for multiple items, and setting the edit mode to list/detail (rather than editing all the items at once).

When the page loads, this region will be created at set up, if it doesn’t already exist.

Refresh the page, check that it shows up in admin, and add a few products to test with – you’ll need them in a moment so that you know it’s all working.

## Choosing a mode – list or detail?

We next need to add some logic to the page to decide whether to show list mode or detail mode. We’ll do that by looking to see if there’s a product slug on the page URL. We do that with `perch_get()`, which is a helper function that looks for items on the query string.

    <?php
    if (perch_get('s')) {

     // Detail mode

    } else {

     // List mode

    }

  ?>

The logic says “if s=something is set on the query string, show detail mode, otherwise, show list mode”.

## Adding the list code

We’re going to use `perch_content_custom()` to show the list code. All we need it to do is show the region using the list template.

    perch_content_custom('Products', array(
     'template' => 'product_listing.html',
    ));

This goes in the ‘else’ section:

    <?php
    if (perch_get('s')) {

     // Detail mode

    } else {

     // List mode
     perch_content_custom('Products', array(
          'template' => 'product_listing.html',
     )); 
    }

    ?>

If you load your page in the browser, you should see your test products listed. Click through to one of them, and should get nothing… yet. Note how the URL now has a s= query string parameter that contains your product slug. It’s this that we’ll use to filter the detail view to show just one product.

## Adding the detail code

To display the detail view of a single product, we need to get clever. We know the ‘slug’ from the value of s= on the query string. We need to feed that into a filter with `perch_content_custom()`

    perch_content_custom('Products', array(
     'template' => 'product_detail.html',
     'filter' => 'slug',
     'match' => 'eq',
     'value' => perch_get('s'),
     'count' => 1,
    ));

As this is the detail view, we’ve chosen the product_detail.html template to use. The filter, match and value options are saying “find any items where the slug is equal to whatever s= is on the query string”. And then just to be sure, we set the count to 1, as we only every want to output a single item here.

This goes in the top half of the if block:

    <?php
    if (perch_get('s')) {

     // Detail mode
     perch_content_custom('Products', array(
          'template' => 'product_detail.html',
          'filter' => 'slug',
          'match' => 'eq',
          'value' => perch_get('s'),
          'count' => 1,
     )); 
    } else {

     // List mode
     perch_content_custom('Products', array(
          'template' => 'product_listing.html',
     )); 
    }

    ?>

Reload your previously empty ‘detail’ page in the browser, and you should see your content appear. That’s it, we’re done!

[Download the files for this solution](../f/download-list-detail.zip)