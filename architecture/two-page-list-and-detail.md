Created by: Drew McLellan
Created date: 2012-05-31
Last updated: 2014-03-11
Authors: Drew McLellan, Rachel Andrew
Title: How do I create two-page list and detail pages?
Tags: multiple item region, perch_content_custom

# How do I create two-page list and detail pages?

## Sometimes you want to have two different files handling list and detail duties. Here's how to set it up.

In [Creating List and Detail Pages](/architecture/how-do-i-create-list-detail-pages) we set up a single page that could act in both list and detail mode. Sometimes it’s desirable to have two different pages perform those tasks.

The key tasks are:

1. Move the detail code onto its own page
2. Update the detail code to reference the region on the listing page
3. Update the listing template to link to the new page for detail links

## Setting up the pages

In the previous example, we had the page `products.php` working in both list and detail mode. This time we’ll use `products.php` to act as the list page, and `product.php` as the detail page.

The list page, `products.php` has two jobs:

1. To create and hold the region containing the content
2. To show the list of products, each linking through to the detail page

The detail page, `product.php` does just one thing; show the detail of the product.

## The list page

Just as before, the list page needs to create the content region to hold the items.

	<?php
	perch_content_create('Products', array(
	     'template'   => 'product_detail.html',
	     'multiple'    => true,
	     'edit-mode' => 'listdetail',
	));
	?>

Then we need to add the list code.

	perch_content_custom('Products', array(
	     'template' => 'product_listing.html',
	));

## The detail page

The detail page needs to use the detail code as before, but this time adding a new option. We need to set the page option to point to the location of the listing page. This is because the region that holds the content lives on the listing page. In order to display the content, we need to tell Perch which page to get it from.

The page option needs a root-relative path, so it always starts with a forward-slash.

	perch_content_custom('Products', array(
	     'page' => '/products.php',
	     'template' => 'product_detail.html',
	     'filter' => 'slug',
	     'match' => 'eq',
	     'value' => perch_get('s'),
	     'count' => 1,
	));

In this case, I’m pointing it to `/products.php` to get the content. That means the `products.php` page in the root of the website. If `products.php` were to be in a subfolder, I’d need to adjust the path from the root of the site, e.g. `/what-we-do/products.php`.

## Adjusting the templates

The only thing left to do is change the listing template to make sure it links to the location of the detail page.

Where we previously had a link to the detail view:

	<a href="?s=<perch:content id="slug" type="slug" />"> … </a>

we need to update the href to make sure the page name is included:

	<a href="product.php?s=<perch:content id="slug" type="slug" />"> … </a>

Your two-page list and detail should now be complete.