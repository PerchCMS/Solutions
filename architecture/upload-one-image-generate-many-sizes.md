Created by: Rachel Andrew
Created date: 2014-03-11
Last updated: 2014-03-11
Authors: Rachel Andrew
Title: How do I upload one image but generate multiple sizes for display?
Tags: images

# How do I upload one image but generate multiple sizes for display?

## If you are reusing your content around the site in different templates you may want a range of sizes and even crops for each image. 

In Perch templates you can reuse the ID of any Perch Template Tag. Reusing an ID means that the editor will be prompted to add that content only once rather than needing to repeat it just because it is displayed twice.

For [images](http://docs.grabaperch.com/docs/templates/attributes/type/image/), you can reuse the ID, but also specify different sizes to resize that image to. Perch will then crop the image to each size on upload.

For example, the following template will display one image upload field in admin but will generate three images:

* one will be resized to a maximum 640x480
* the second will be resized to a maximum 320x240
* the third will be a 120x120 crop

    <img src="<perch:content id="main_image" type="image" label="Article image" width="640" height="480" />" alt="<perch:content id="alt" type="text" label="Alt text" />" />
    <perch:content id="main_image" type="image" label="Article image" width="320" height="240" suppress="true" />
    <perch:content id="main_image" type="image" label="Article image" width="120" height="120" suppress="true" />
    
Note that the second and third images have the [suppress attribute](http://docs.grabaperch.com/docs/templates/attributes/suppress/) set to true. This means that the only image that will display on the front end of the site when this template is used, will be the large image. The other images would be for us when the content is represented perhaps on the homepage.