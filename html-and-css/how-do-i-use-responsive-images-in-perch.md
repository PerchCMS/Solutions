Created by: Drew McLellan
Created date: 2012-05-31
Last updated: 2014-03-11
Authors: Drew McLellan, Rachel Andrew
Title: How do I use responsive images in Perch?
Tags: images, RWD, picture element, srcset

# How do I use responsive images in Perch

## If you are following responsive web design techniques then Perch can help you do so. This solution explains how.

At the simplest level, if you have a responsive design then you are likely to not want heights and widths on images. Use the config setting [PERCH_RWD](http://docs.grabaperch.com/docs/installing-perch/configuration/markup/) set to true and where image tags are created they will not include height or width.

The [Responsive Images Community Group](http://responsiveimages.org/) currently has two markup-based proposals for responsive images. Both of these can be delivered, today, with dynamic content using Perch templates. Let’s take a look at how.

## The picture Element

The first proposed markup pattern is the picture element. The sample markup looks like this:

    <picture>
      <source media="(min-width: 40em)" srcset="big.jpg 1x, big-hd.jpg 2x">
      <source srcset="small.jpg 1x, small-hd.jpg 2x">
      <img src="fallback.jpg" alt="">
    </picture>

This uses source elements to serve images to browsers that understand the picture element, but falls back to a regular image tag for those that don’t. In Perch, you can have your client upload just one image and have the different formats automatically created for them. The template would look like this:

    <picture>
      <source media="(min-width: 40em)" srcset="<perch:content id="img" type="image" width="1024" /> 1x, 
          <perch:content id="img" type="image" width="1024" density="2" /> 2x">
      <source srcset="<perch:content id="img" type="image" width="640" /> 1x, 
          <perch:content id="img" type="image" width="640" density="2" /> 2x">
      <img src="<perch:content id="img" type="image" label="Image" order="1" width="640" />" alt="">
    </picture>

(Of course, you’d want to drop a field in that alt attribute, too.)

What we’re doing here is sizing the image to a width of 1024 for the ‘big’ version, and using the density attribute to create the 2x version. For the ‘small’ version, we’re sizing it to 640 wide, and then also reusing that size as the fallback default.

The density attribute on a image acts as a multiplier on the dimensions you give. If an image is scaled to a width of 1024 with density="2", Perch will actually scale it to 2048, but when asked will output a width value of 1024. It does more than save you some mental arithmetic, though, as it performs the same multiplication on the height, which you can’t know at the time of writing the template.

You could, of course, use two different images if you wanted the editor to be able to exercise editorial control over the big vs small image.

## The srcset Attribute

The second proposed pattern uses a regular image tag, but adds a new srcset attribute. The sample markup looks like this:

    <img src="fallback.jpg" alt="" srcset="small.jpg 640w 1x, small-hd.jpg 640w 2x, med.jpg 1x, med-hd.jpg 2x ">

Following the same process, your Perch template would look like this:

    <img src="<perch:content id="img" type="image" label="Image" order="1" width="640" />" alt="" 
      srcset="<perch:content id="img" type="image" width="640" /> 640w 1x, 
        <perch:content id="img" type="image" width="640" density="2" /> 640w 2x, 
        <perch:content id="img" type="image" width="1024" /> 1x, 
        <perch:content id="img" type="image" width="1024" density="2" /> 2x ">

Again, don’t forget the alt in your own templates.

Obviously, the srcset pattern is less structured (and so perhaps easier to make mistakes), but ends up easier to read back.

Whichever pattern for responsive images catches on in the end (even if it’s neither of these) we aim to make it easy to use with Perch.