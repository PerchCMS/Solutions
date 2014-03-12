Created by: Rachel Andrew
Created date: 2014-03-12
Last updated: 2014-03-12
Authors: Rachel Andrew
Title: How do I add help text to my edit forms?
Tags: templates

# How do I add help text to my edit forms?

## You would like to add some information to help your content editors use the edit forms.

We've tried to make it possible for you to really guide your content editors through their use of Perch. Once way is to add help text to edit forms and individual fields.

To add a block of help text at the top of an edit for use the perch:help tag.

    <perch:help>
    <p>Any amount of HTML-formatted help can be specified here, including images and links if required.</p>
    </perch:help>

To add help next to a certain field use the help attribute on that field.

    <perch:content type="text" id="heading" label="Heading" 
  help="Give the article a descriptive title" />

Adding help text in this way can really aid in enforcing the content strategy for your site.