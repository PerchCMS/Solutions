Created by: Drew McLellan
Created date: 2014-07-09
Last updated: 2014-07-09
Authors: Drew McLellan
Title: How do I create links to previous and next items?
Tags: multiple item region, perch_content_custom

# How do I create links to previous and next items?

## When using a multiple item region, particularly with a list/detail display, it is sometimes useful to be able to link to the next or previous item in that region. This can be done with some simple filtering and ordering using `perch_content_custom()`

Here's the scenario; we have a multiple item region set up using the [list and detail](/architecture/how-do-i-create-list-detail-pages) approach. On the detail page, it would be great to be able to show links to the previous and next items in the list, with the user needing to navigate back to the list to find them.

To do this we need three `perch_content_custom()` calls:

1. The original call that finds the main item we're looking at
2. A call to find the previous item
3. A call to find the next item

## Modifying the main call

Taking the example from the [list and detail](/architecture/how-do-i-create-list-detail-pages) solution, our `perch_content_custom()` call used to show the detail view looks like this:

~~~
perch_content_custom('Products', array(
    'template' => 'product_detail.html',
    'filter'   => 'slug',
    'match'    => 'eq',
    'value'    => perch_get('s'),
    'count'    => 1,
));
~~~

We need to make an important change to this in order to have the information we need to find the next and previous items. We need to use the `skip-template` option to return the raw content, and then use the `return-html` option to make sure we get the HTML back too.

The result loooks like this:

~~~
$result = perch_content_custom('Products', array(
    'template'      => 'product_detail.html',
    'filter'        => 'slug',
    'match'         => 'eq',
    'value'         => perch_get('s'),
    'count'         => 1,
    'skip-template' => true,
    'return-html'   => true,
));
~~~

Because of the `skip-template`, this call won't output anything to the page. We need to do that with a simple `echo` statement:

~~~
echo $result['html'];
~~~

This leaves us with the main detail item being output to the page just as before, but now we have the raw content fields also available to us in the variable `$result`.

## Creating the template

To show the previous and next items, we need a template. This can be anything from a simple link, to a mini preview of the content item. You have the full range of content available, including images and so on.

Save this as `product_prevnext.html` in your templates folder.

~~~
<a href="?s=<perch:content id="slug" type="slug" />">
    <perch:if exists="is_prev">Previous<perch:else />Next</perch:if>:
    <perch:content id="image" type="image" width="100" height="100" crop="true" output="tag" />
    <perch:content id="title" type="text" />
</a>
~~~

## Finding the Next item

To find the next item, the logic is simple:

1. Sort the region
2. Filter for just the items that come _after_ our main item in the list
3. Take the first one of those left

Remember we have our main item stored in the variable `$result`, so we can make use of that here.

~~~
perch_content_custom('Products', array(
    'template'   => 'product_prevnext.html',
    'filter'     => '_order',
    'match'      => 'gt',
    'value'      => $result[0]['_sortvalue'],
    'sort'       => '_order',
    'sort-order' => 'ASC',
    'count'      => 1,
));
~~~

There's a neat trick at play here. We're filtering on a special value of `_order`. This is the 'natural' order of the items within the region. According to this filter, the `_order` needs to be greater than (`gt`) the `_sortvalue` of the main item.

`_sortvalue` is the other part of the trick. This is the value that was used for sorting when the main item was found. So if it was found using the natural order (no sort value) then it would be its `_order`. If you sorted by another field, say price, then `_sortvalue` would be the price. This enables you to figure out a relational order between items no matter how they're sorted.

We're sorting by the regions natural order, and filtering where the position in that order is greater than the main item's position. And then just taking the first result.

## Finding the Previous item

The process for the previous item is just the same, but we reverse the filtering and ordering. We need to find the items whose order puts them before our main item in the list, and then just pick off the last one. We don't have the tools to pick off the last one, so we reverse the order (`'sort-order'=>'DESC'`) and pick off the first.

We also need to set that `is_prev` value that our template is using to display the correct labels.

~~~
PerchSystem::set_var('is_prev', true);

perch_content_custom('Products', array(
    'template'   => 'product_prevnext.html',
    'filter'     => '_order',
    'match'      => 'lt',
    'value'      => $result[0]['_sortvalue'],
    'sort'       => '_order',
    'sort-order' => 'DESC',
    'count'      => 1,
));
~~~

That gives us our previous item.

## Sorting by a particular field

If you want to sort the region by something other than its natural order, you just need to set the same `sort` option on all three `perch_content_custom()` calls, and update the `filter` on the previous and next items to use that field too.