Created by: Rachel Andrew
Created date: 2014-03-11
Last updated: 2014-03-11
Authors: Rachel Andrew
Title: How do I create a Field Type
Tags: field types, templates

# How do I create a Field Type?

## In Perch, every content template tag has a type attribute. This specifies which type of field is used to collect and process the data. In this solution we explain how to start creating your own.

In Perch, every content template tag has a type attribute. This specifies which type of field is used to collect and process the data. From text to textarea, checkbox to file, these all have different form controls and ways of handling the data. In Perch 2, you can create your own field types.

Creating a field type is a simple way to start extending Perch as all you need to create is one PHP class that defines the fields needed to collect the data and the code to process it. This solution will show you how to create a simple field type that creates a list of the files you have uploaded to your Perch resources folder, enabling the editor to select one.

You can download my fully worked example below.

[Filelist Field Type example](../f/download-create-a-field-type.zip)

My example Field Type has been commented to explain what the main elements of the Field Type do. To use the Field Type open `perch/addons/fieldtypes` and put the folder filelist containing filelist.class.php into it. You can then use it like any other Field Type.

As explained in the documentation for Field Type, my class has the required four main functions:

* *render_inputs()* – this function displays the edit page in Perch admin
* *get_raw()* – reads in the form data when submitted and processes it
* *get_processed()* – gets the data ready for templating
* *get_search_text()* – hands something to the search index so the content of this field can be searched

The above functions are detailed in the Field Type documentation and the example `filelist.class.php` is documented to show how they work in practice.

I also have a function `_get_files`, this function is to enable the functionality of my Field Type, it looks in the perch/resources folder and returns a list of all files (if a file extension has not been passed to it) or a list of just those files that have a particular extension.

You can add as many functions as you need in your class as long as you also have those that are required by Perch.

You will generally find that you can use the example FieldType that ships with Perch, or the example from this solution and then start to tweak it for your own purposes.