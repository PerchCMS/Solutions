Created by: Rachel Andrew
Created date: 2014-03-11
Last updated: 2014-03-11
Authors: Rachel Andrew
Title: How do I create unique IDs in a multiple-item region
Tags: templates

# How do I create unique IDs in a multiple-item region?

## If you need each item displayed with a multiple item region to have a unique ID then perch_item_index will help.

Sometimes, when outputting a multiple item region, it’s useful to be able to number the items. That might be to help with a design element on the page, or even to output unique, sequential IDs to help with some JavaScript.

You can do this in your template using the special ID value [perch_item_index](http://docs.grabaperch.com/docs/templates/attributes/id/).

    <div id="item<perch:content id="perch_item_index" />">
      ...
    </div>

For each content item output by the template, Perch will increment the number by one. The above would result in:

    <div id="item1">
      ...
    </div>
    <div id="item2">
      ...
    </div>
    <div id="item3">
      ...
    </div>

One thing that’s important to remember, is that `perch_item_index` is a sequential count of the items as they are output. If items are added or removed, or the ordering is changed, then the number output by `perch_item_index` will change correspondingly.