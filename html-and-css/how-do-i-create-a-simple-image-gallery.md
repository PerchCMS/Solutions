# How do I create an image gallery?

## Perch has a feature complete Gallery app, however sometimes all you need is a basic listing of images that you can combine with a jQuery plugin to make a simple slideshow.

Perch has a feature complete Gallery app, however sometimes all you need is a basic listing of images that you can combine with a jQuery plugin to make a simple slideshow.

This solution demonstrates how to use Perch to create a list of thumbnails that link to larger images.

In your page, create a new region called Gallery, wrapping it in an unordered list. This region will contain our thumbnails as list items.

    <ul>
      <?php perch_content('Gallery'); ?>
    </ul>

Next, we need to create a custom template for this region to use. Create a new file inside perch/templates/content and call it gallery_image.html.

Each item in the region will be a list item containing a thumbnail image which links to the larger version. So the outline of the HTML for the template will look like this:

    <li>
      <a href="">
        <img src="" alt="" />
      </a>
  </li>

The src of the image needs to be an image file, so we’ll add that first.

When you use a type of image in a Perch Content tag this does not give you an image HTML tag, rather it return the src attribute as seen below. This means you need to create a template uses this tag.

    <li>
      <a href="">
        <img src="<perch:content id="image" type="image" label="Image" width="75" height="75" crop="true" />" alt="" />
      </a>
    </li>

I have decided to create square thumbnails, no matter what the dimensions of the uploaded image. So I set the width and height to 75 pixels and crop to true.

The href of the link needs to point to a larger version of the file. If we reuse the same ID for a second image, Perch will only prompt the user to upload one file, but will process it in two different ways.

    <li>
      <a href="<perch:content id="image" type="image" label="Image" width="800" height="600" />">
        <img src="<perch:content id="image" type="image" label="Image" width="75" height="75" crop="true" />" alt="" />
      </a>
    </li>

This time we’ve set a maximum dimension of 800 pixels for the width and 600 pixels for the height height, but not set it to crop – this will resize the image but keep its natural ratio. (It’s always worth setting some dimensions unless you really want to let content editors upload enormous images!)

The final step is to add a regular text field for the alt attribute and set it to be required.

    <li>
      <a href="<perch:content id="image" type="image" label="Image" width="800" height="600" />">
        <img src="<perch:content id="image" type="image" label="Image" width="75" height="75" crop="true" />" 
             alt="<perch:content id="title" label="title" type="text" required="true" />" />
      </a>
    </li>

Save your template, and choose it to use for your Gallery region, allowing multiple items. Then add a few images.

If you go back to your PHP page and refresh you should see a list of square images, clicking on any image will take you to the larger version.

Obviously, this basic implementation works just fine for users without JavaScript, but some real polish and flare can then be added with the use of something like Fancybox for jQuery or something similar for your favourite JavaScript library.

If you are having problems with uploading and resizing images this is often down to configuration of your hosting. Check the troubleshooting tips for images in the documentation for help.