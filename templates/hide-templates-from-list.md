Created by: Rachel Andrew
Created date: 2014-03-12
Last updated: 2014-03-12
Authors: Rachel Andrew
Title: How do I hide templates from the list in the Control Panel?
Tags: templates

# How do I hide templates from the list in the Control Panel?

## If you are using templates for perch_content_custom you probably don't want these cluttering the select list when setting up a region.

To hide templates from the list in the Control Panel, start the template name with an underscore. The following template **will** appear in the list:

    my_custom_template.html

Rename it with an underscore at the start and it **will not** appear but still be accessible from `perch_content_custom`.

    _my_custom_template.html