Created by: Drew McLellan
Created date: 2012-05-31
Last updated: 2014-03-11
Authors: Drew McLellan
Title: How do I use compressive images in Perch?
Tags: images, RWD, picture element, srcset

# How do I use compressive images in Perch?

## In their blog post Compressive Images, the Filament Group describe how a large image, heavily compressed and shown scaled down in the browser can result in a higher quality image without a big hit on file size. Sometimes even with a file size reduction.

You can [read the full post](http://filamentgroup.com/lab/rwd_img_compression/) for the lowdown. This is particularly useful for responsive design, where you might want to enable images to scale up and down, and when targeting hi-DPI screens like Apple’s Retina displays.

So how would you do that with a Perch template? There’s a few attributes on the image tag that can help. Let’s take a really basic image field as a starting point. We’ll use the output="tag" attribute to have Perch output an entire image tag for us:

	<perch:content id="img" type="image" label="Image" output="tag" width="400" />

We’re scaling the image down to 400px wide.

The two main characteristics of the compressive image technique are that the image is larger than it’s displayed, and that it’s more heavily compressed. The image field type has three attributes that help with that.

* `density` -- set the pixel density of the image vs its display size, so makes the image bigger than it’s displayed
* `quality` -- sets the compression level. It’s a value from 0 to 10.
* `sharpen` -- sets the amount of sharpening added to the image. Again, 0 to 10, this defaults to 4. We can reduce the sharpening to lower the image quality.

Applying those gives us a template tag like this:

	<perch:content id="img" type="image" label="Image" output="tag" width="400" density="2" quality="30" sharpen="2" />

Setting the density to 2 makes the image file twice as big (800px wide). A quality of 30 makes it quite heavily compressed, and the sharpening can be reduced to 2 without too much definition being lost.

The exact values to use can depend roughly on the sorts of images and the intended purpose. A photographer’s portfolio would benefit from better quality at the expense of file size, whereas a news site might sacrifice more quality for speed. The above settings give me images of the same file size, the same appearance on regular screens, and a better quality image on a Retina display.