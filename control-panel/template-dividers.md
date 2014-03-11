Created by: Rachel Andrew
Created date: 2014-03-11
Last updated: 2014-03-11
Authors: Rachel Andrew
Title: How do I split up the admin editing page into sections?
Tags: admin, editing, templates

# How do I split up the admin editing page into sections

## If you have created a complex editing form it can be helpful to your editors to split it up into sections. The divider attribute can help you to do that.

Dividers let you split up a complex template into sections, creating a divider bar and heading in the UI.

To use Template Dividers you can select a template tag that you want the Divider to display after and use the attribute `divider-before` with a value that will display as text in the bar.

    <perch:content id="text" type="textarea" label="Text" textile="true" 
editor="markitup" divider-before="Important information" />

Or you can use `divider-after` in the same way.

    <perch:content id="text" type="textarea" label="Text" textile="true" 
editor="markitup" divider-after="Related material" />