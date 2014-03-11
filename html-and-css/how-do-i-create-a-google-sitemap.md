Created by: Drew McLellan
Created date: 2012-05-31
Last updated: 2014-03-11
Authors: Drew McLellan
Title: How do I create a Google Sitemap?
Tags: XAMPP, local development, PHP

# How do I create a Google Sitemap

## Sitemaps are an easy way for webmasters to inform search engines about pages on their sites that are available for crawling. In its simplest form, a Sitemap is an XML file that lists URLs for a site along with additional metadata about each URL (when it was last updated, how often it usually changes, and how important it is, relative to other URLs in the site) so that search engines can more intelligently crawl the site.

[Sitemaps](http://www.sitemaps.org/) are an easy way for webmasters to inform search engines about pages on their sites that are available for crawling. In its simplest form, a Sitemap is an XML file that lists URLs for a site along with additional metadata about each URL (when it was last updated, how often it usually changes, and how important it is, relative to other URLs in the site) so that search engines can more intelligently crawl the site.

Whilst a fully featured Sitemap is quite a bit of work, Perch can create a simple Sitemap automatically and easily using the navigation functionality.

## Create a navigation template

First, create a new navigation template at perch/templates/navigation/sitemap.html containing the following.

    <perch:before><?xml version="1.0" encoding="UTF-8"?>
    <urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
    </perch:before>
    <url>
    	<loc>http://example.com<perch:pages id="pagePath" /></loc>
    </url>
    <perch:after>
    </urlset>
    </perch:after>

Update the template to contain your URL rather than example.com and save it.

## Create the sitemap page

Normally, the convention is to create your Sitemap as sitemap.xml at the root of your site. See Using Different File Extensions for how to configure Perch to run without a .php extension.

For now, create your file as sitemap.php at the top level of your website.

The first thing this file does is set the Content-type header to state that it’s an XML document. Then it just includes the Perch runtime, and called perch_pages_navigation() to output the site structure using the sitemap.html template we created.

    <?php
	    header('Content-type: application/xml');
	    include('perch/runtime.php');
	    perch_pages_navigation(array(
		    'template'=>'sitemap.html',
		    'flat'=>true
		  ));
    ?>

That should be it – you now have a basic, but fully functional Sitemap which can be submitted to Google using the Web Master Tools.