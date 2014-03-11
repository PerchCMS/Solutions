Created by: Rachel Andrew
Created date: 2014-03-11
Last updated: 2014-03-11
Authors: Rachel Andrew
Title: How do I change the size of textareas in the admin?
Tags: admin, editing, templates

# How do I change the size of textareas in the admin?

## You can use "t-shirt sizes" to create appropriately sized textareas for your content.

One of the great strengths of Perch is the flexibility to construct content forms that match the nature of your content. Often you know when a field like a textarea should expect a little or a lot of content.

A perfect example of this a news article – you might have a big textarea for the main body of the article, and a much smaller one for an introductory paragraph used for a listing elsewhere on the site.

You can set the size of a textarea in your template:

    <perch:content type="textarea" size="xl" id="news_article" label="Main article" />

The size options are based on t-shirt sizes: xs,s, m, l, xl and xxl. You can read about the other options for textareas on the [textarea documentation page](http://docs.grabaperch.com/docs/templates/attributes/type/textarea/).