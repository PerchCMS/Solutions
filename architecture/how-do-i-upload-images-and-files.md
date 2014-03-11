Created by: Rachel Andrew
Created date: 2012-05-31
Last updated: 2014-03-11
Authors: Rachel Andrew, Drew McLellan
Title: How do I let content editors add images and files?
Tags: images, files

# How do I let content editors add images and files?

## This solution details how to give your editors the ability to upload images and files in the Perch admin.

There are a couple of ways in which Perch can be used to enable your client to add images and files to their content, either by using the file and image Perch Content tags or by allowing them to upload images inline using an editor.

## Using the Perch Content tags

Perch Content tags are used in your templates when defining content to be added by an editor. For example you might have a template with a heading, and image and a large block of text. See the video on Creating Templates to see how templates work in Perch.

A Perch File Content Tag looks like this:

    <perch:content id="report" type="file" label="Annual report PDF" />

This will present a file upload field in the administration form and the editor can upload an image from their computer. When displayed on your site this will create a link to the file, stored in the Perch resources folder.

A Perch Image Content Tag looks like this:

    <perch:content id="logo" type="image" label="Logo" />

Just as with a file tag, this will present a file upload field in the administration form and the editor can upload an image from their computer. It is most likely that you will want to have some control over the dimensions of the image and so you can set the following attributes:

* width
* height
* crop

Setting width and height will scale the image. If you only set width then the image ratio will remain the same to scale the height, likewise if you set height we will scale the image within the correct ratio to get the width. If you want to force the image to a certain width AND height (for example making a square thumbnail) you need to set both width and height and also set the attribute crop to true.

    <perch:content id="thumbnail" type="image" label="Thumbnail" width="40" height="40" crop="true" />

### Using the standard MarkItUp! Editor

The editor included in Perch has the ability to upload files into a textarea content block in Perch. Images can be optionally resized by using the imagewidth, imageheight and imagecrop attributes on the textarea content tag.

### Using ckEditor

We have configured the ckEditor image upload button to also allow images uploads in Perch, this opens a modal dialogue and is standard ckEditor functionality.

## Which should you use?

If you want to have full control over the placement of your images then using the Perch Content Tags gives the best control. You get to choose where on the page the image sits and how it falls in the layout with other things around it.

If however you just want your client to be able to add images inline of a blog post or page of text then the options to use MarkItUp or ckEditor can be very helpful, you can of course mix both methods across a site using Perch or even on one page.

## Potential problems with image and file uploads

Uploading images and files is one place where we see problems based on the various ways hosting accounts are configured. Shared hosting is often configured with very low upload limits, so you may find you cannot upload an image greater than 2MB for example. Perch cannot override this setting. You can find out what your hosting is limited to by looking in your Diagnostic Report under Settings.

Perch relies on one of the two most common image libraries being installed on your server. These are GD and ImageMagick. The Compatibility Test will tell you if you do not have one or other of these libraries – it is unusual to find shared hosting that does not support this.