Created by: Rachel Andrew
Created date: 2014-03-12
Last updated: 2014-03-12
Authors: Rachel Andrew
Title: How do I create an excerpt?
Tags: templates, words, chars

# How do I create an excerpt?

## When redisplaying content, or creating a list/detail page it can be helpful to show an excerpt rather than all of the content entered into a particular field.

Using the `chars` attribute tells the template engine to only show that number of characters when rendering the field:

    <perch:content type="text" id="heading" label="Heading" chars="100" />

The `words` attribute has the same effect, this time restricting the number of words:

    <perch:content type="text" id="heading" label="Heading" words="20" />

In both cases you can use the `append` attribute to add `...` or anything else to the end of the string to show it is an excerpt.

    <perch:content type="text" id="heading" label="Heading" words="20" append="..." />

There is information about [words](http://docs.grabaperch.com/docs/templates/attributes/words/) and [chars](http://docs.grabaperch.com/docs/templates/attributes/chars/) in the Perch documentation.
