Created by: Drew McLellan
Created date: 2012-05-31
Last updated: 2014-03-12
Authors: Drew McLellan
Title: Adding Facebook Like buttons to a page
Tags: facebook

# Adding Facebook Like buttons to a page

## Integration with social media sites is an increasingly important tool for driving traffic to your site. This solution explains how to add Facebook 'Like' buttons to a page.

Adding a Facebook ‘Like’ button to a page is fairly straightforward. The first point of reference is Facebook’s own developer documentation which contains sample code for adding a like button.

The HTML5 version of the code includes two parts. The first part is the Facebook JavaScript SDK which needs to be included once on the page.

	<div id="fb-root"></div>
	<script>(function(d, s, id) {
	  var js, fjs = d.getElementsByTagName(s)[0];
	  if (d.getElementById(id)) return;
	  js = d.createElement(s); js.id = id;
	  js.src = "//connect.facebook.net/en_US/all.js#xfbml=1";
	  fjs.parentNode.insertBefore(js, fjs);
	}(document, 'script', 'facebook-jssdk'));</script>

Then, at the point you want to insert a Like button, you need the following snippet.

	<div class="fb-like" data-send="true" data-width="450" data-show-faces="true"></div>

This could be added to your blog’s post.html template, for example.

By default, the button with ‘like’ the current page. If you want to like a different page, you can set that with the data-href attribute

	<div class="fb-like" data-href="http://grabaperch.com" data-send="true" data-width="450" data-show-faces="true"></div>

There are various options, listed in the Facebook documentation

There’s no reason this couldn’t be used in a Perch template, to set the options dynamically.

	<div class="fb-like" data-href="<perch:content id="url" type="url" label="URL to like" />" data-send="true" data-width="450" data-show-faces="true"></div>