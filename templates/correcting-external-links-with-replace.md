Created by: Rachel Andrew
Created date: 2014-03-12
Last updated: 2014-03-12
Authors: Rachel Andrew
Title: How do I make sure people enter correct links to a website address?
Tags: templates

# How do I make sure people enter correct links to a website address?

## Content editors sometimes forget to add a full website address including the http:// leaving you with broken links on the site. 

You can use the `replace` attribute on a template tag to ensure that you end up with an http:// at the beginning of a URL.

Firstly add `http://` to the beginning of the link, this will ensure that all links start with `http://`. You now need to deal with the fact that some editors will add the http:// and you don't want it to appear twice.

On the template tag used to collect this information add the replace attribute with a value of `http://|`. This tells Perch that if it finds the string http:// in the field to replace it with nothing when displaying it.

    <a href="http://<perch:content id="url" type="text" label="Your website" replace="http://|" />">

