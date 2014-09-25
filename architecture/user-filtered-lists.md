Created by: Drew McLellan
Created date: 2014-09-04
Last updated: 2014-09-04
Authors: Drew McLellan
Title: How do I create a user-filterable list?
Tags: templates, perch_content_custom

# How do I create a user-filterable list?

## You can a region that you'd like the website visitor to be able to filter using a form. Here's how to do it using multiple dynamic filters.

It's a faily common scenario that you have a long list of items that you'd like the user to be able to search (or more accurately, filter) using a form on the page. In this example, we'll take a real estate listing.

Our region, _Properties_, contains a large number of houses, apartments and studios. It has fields for the number of bedrooms, the location (inner city or suburbs) and the price.

Normally, we'd display the listing like this:

~~~ 
perch_content_custom('Properties', array(
    'template'   => 'property_listing.html',
    'sort'       => 'price', 
    'sort-order' => 'DESC',
));
~~~

This lists all our properties, most expensive to least expensive.

## Creating a filtering form

The first thing to do is create a form on the page for the user to make their selections.

Install the Forms app if you haven't already, as this gives us access to the handy `perch_form()` function for displaying forms without needing a content region.

In your page:

~~~
perch_form('property_filter.html');
~~~

Then create a new file at `perch/templates/forms/property_filter.html` and start building up your form.

~~~
<perch:form id="filter" method="get">
	<div>
		<perch:label for="type">Type</perch:label>
    	<perch:input type="select" id="type" options=",House|house,Apartment|apartment,Studio|studio" />
    </div>
	<div>
		<perch:label for="beds">Bedrooms</perch:label>
    	<perch:input type="select" id="beds" options=",1,2,3,4" />
    </div>
    <div>
		<perch:label for="location">Location</perch:label>
    	<perch:input type="select" id="location" options=",City|city, Suburbs|suburbs" />
    </div>
    <div><perch:input type="submit" value="Filter" /></div>
</perch:form>
~~~

You want to add fields for each thing you want to filter by. This form uses the `GET` HTTP method, so when it's submitted, the chosen options will be added to the URL as a query string, something like:

    ?beds=3&location=city
    
## Filtering from the URL options

Once you have the options set on the URL, you can create your filters.

~~~
// Create an empty array ready to add our filters to
$filters = array();

if (perch_get('type')) {
	// if 'type' is on the URL, add a filter for bedrooms
	$filters[] = array(
		'filter' => 'type',
		'match'  => 'eq',
		'value'  => perch_get('type'),
	);
}

if (perch_get('beds')) {
	// if 'beds' is on the URL, add a filter for bedrooms
	$filters[] = array(
		'filter' => 'beds',
		'match'  => 'eq',
		'value'  => perch_get('beds'),
	);
}

if (perch_get('location')) {
	// if 'location' is on the URL, add a filter for the location
	$filters[] = array(
		'filter' => 'location',
		'match'  => 'eq',
		'value'  => perch_get('location'),
	);
}

// Unset the filters if none are used:
if (!count($filters)) $filters=false;

// Then get the list
perch_content_custom('Properties', array(
    'template'   => 'property_listing.html',
    'sort'       => 'price', 
    'sort-order' => 'DESC',
    'filter'     => $filters,
));
~~~
