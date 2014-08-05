Created by: Drew McLellan
Created date: 2012-05-31
Last updated: 2014-08-04
Authors: Drew McLellan, Rachel Andrew
Title: How do I use responsive images in Perch?
Tags: images, RWD, picture element, srcset

# How do I use responsive images in Perch?

## You would like to ensure that as browsers begin to support the new picture element that your site takes advantage of it.

The _picture_ element, a method for using true responsive images on the web, is now making it's way into browsers. Perch makes it easy to use this new element in your designs so that as browsers start to add support your site will allow visitors to benefit.

## First steps to responsive images

At the simplest level, if you have a responsive design then you are likely to not want heights and widths on images. Use the config setting [PERCH_RWD](http://docs.grabaperch.com/docs/installing-perch/configuration/markup/) set to true and where image tags are created they will not include height or width and the image will be able to respond to browser width.

## The picture Element

The picture element covers a range of use cases. It gives you the ability to change image sizes based on responsive design rules, optimise images for high-dpi screens, serve images with different mime types and even to display different versions of an image descending on context. For example rather than just displaying a squished down big image on a mobile phone you might opt to show a cropped version.

Perch works really well in combination with the picture element to help you communicate to content editors what is required for your design.

In this solution I have taken some of the examples used in [this post on Dev.Opera](http://dev.opera.com/articles/responsive-images/). I'm showing the markup, and then a Perch template that would give you this output.

In practice you would most likely be including the picture element within a larger template with other field types, to make up an article, post or product listing.

## Art direction use case

In this case you want the content editor to upload two images. One will be used for large screens (wider than 1024 pixels) and the other a prepared crop for small screens. We use help text to guide the editor.

### Output HTML

    <picture>
	    <source media="(min-width: 1024px) srcset="opera-fullshot.jpg">
	    <img src="opera-closeup.jpg" alt="The Oslo Opera House">
    </picture>

### Perch template

    <picture>
	    <source media="(min-width: 1024px)" srcset="<perch:content type="image" id="image" label="Image" help="Full size image for large screens" />">
	    <img src="<perch:content type="image" id="imagecloseup" label="Closeup image" help="Closeup image for small screens, will be resized down to 1024 pixels" width="1024" />" alt="<perch:content type="text" id="alt" label="Description" required="true" help="Description of subject of these images." title="true" />">
    </picture>

## Different image types use case

In this case you want the content editor to upload a webp image for browsers that support it and a JPG or other format for the others.

_**Note**: support for webp is coming to PHP. At the moment in Perch our suggestion is to use a file upload type in order that your file does not get mangled._

### Output HTML

    <picture>
	    <source srcset="opera.webp" type="image/webp">
	    <img src="opera.jpg" alt="The Oslo Opera House">
    </picture>

### Perch Template

    <picture>
      <source srcset="<perch:content type="file" id="webp" label="Webp Image" help="Webp image type for supporting browsers." />" type="image/webp">
      <img src="<perch:content type="image" id="image" label="Image" help="Image for broswers without webp support" />" alt="<perch:content type="text" id="alt" label="Description" required="true" help="Description of subject of these images." title="true" />">
    </picture>

## High-DPI images use case

In this case we want our content editors to only upload one image. Perch will then create three images - a standard one plus two higher DPI images.

We use the density attribute of the perch:image tag and reuse the id of the image, in order that Perch will know to present just one upload field but create the different images specified.

The density attribute on a image acts as a multiplier on the dimensions you give. If an image is scaled to a width of 1024 with density="2", Perch will actually scale it to 2048, but when asked will output a width value of 1024. It does more than save you some mental arithmetic, though, as it performs the same multiplication on the height, which you can’t know at the time of writing the template.

### Output HTML

    <img src="opera-1x.jpg" alt="The Oslo Opera House"
	srcset="opera-2x.jpg 2x, opera-3x.jpg 3x">

### Perch template

    <img src="<perch:content id="image" type="image" width="1024" label="Image" />" alt="<perch:content type="text" id="alt" label="Description" required="true" help="Description of this image" title="true" />" srcset="<perch:content id="image" type="image" width="1024" label="Image" density="2" /> 2x, <perch:content id="image" type="image" width="1024" label="Image" density="3" /> 3x">

## High-DPI images & art direction use case

In this case we want to combine art direction - uploading a specific crop for smaller screens with the high-DPI technique. Our content editor will need to upload two images - Perch will create 6.

### Output HTML

    <picture>
	    <source media="(min-width: 1024px)"
		  srcset="opera-fullshot-1x.jpg 1x,
			  opera-fullshot-2x.jpg 2x,
				opera-fullshot-3x.jpg 3x">
	<img src="opera-closeup-1x.jpg" alt="The Oslo Opera House"
		srcset="opera-closeup-2x.jpg 2x,
				opera-closeup-3x.jpg 3x">
    </picture>

### Perch template

    <picture>
	    <source media="(min-width: 1024px)"
		  srcset="<perch:content id="image" type="image" label="Image" help="Full size image for large screens" /> 1x,
			  <perch:content id="image" type="image" label="Image" density="2" /> 2x,
				<perch:content id="image" type="image" label="Image" density="3" /> 3x">
	<img src="<perch:content type="image" id="imagecloseup" label="Closeup image" help="Closeup image for small screens, will be resized down to 1024 pixels" width="1024" />" alt="<perch:content type="text" id="alt" label="Description" required="true" help="Description of subject of these images." title="true" />"
		srcset="<perch:content type="image" id="imagecloseup" label="Closeup image" width="1024" density="2" /> 2x,
				<perch:content type="image" id="imagecloseup" label="Closeup image" width="1024" density="3" /> 3x">
    </picture>


## Changing image sizes use case

In this use case we want to use different image sizes for different browser window widths. Supporting browsers will select the best image to use. We want our content editor to just need to upload one image, in the case of the below template Perch will then create the main image (used as a fallback in non-supporting browsers) and 4 additional images at widths 200 pixels, 400 pixels, 800 pixels and 1200 pixels.

### Output HTML

    <img src="opera-fallback.jpg" alt="The Oslo Opera House"
	sizes="(min-width: 640px) 60vw, 100vw"
	srcset="opera-200.jpg 200w,
			opera-400.jpg 400w,
			opera-800.jpg 800w,
			opera-1200.jpg 1200w">

### Perch template
    
    <img src="<perch:content type="image" id="image" label="Image" help="Upload or select an image" />" alt="<perch:content type="text" id="alt" label="Description" required="true" help="Description of this image" title="true" />"
	sizes="(min-width: 640px) 60vw, 100vw"
	srcset="<perch:content type="image" id="image" label="Image" width="200" /> 200w,
			<perch:content type="image" id="image" label="Image" width="400" /> 400w,
			<perch:content type="image" id="image" label="Image" width="800" /> 800w,
			<perch:content type="image" id="image" label="Image" width="1200" /> 1200w">

## Changing image sizes, high-DPI images and art direction use case

As you have probably realised by now you can combine these techniques as best works for your site and requirements. This final template will require the content editor to upload two images - a full-size image and a crop, just as in the very first example. However Perch will create a whole range of images - the fallback image plus 6 versions of the main image and 6 of the crop. The browser will then select the best one to use keeping in mind image width and screen DPI.

The fantastic thing about this is that your content editor just has to upload or select from Assets two images. Perch and the magic of the picture element will take care of the rest. 

### Output HTML

    <picture>
	    <source
		media="(min-width: 1280px)"
		sizes="50vw"
		srcset="opera-fullshot-200.jpg 200w,
				opera-fullshot-400.jpg 400w,
				opera-fullshot-800.jpg 800w,
				opera-fullshot-1200.jpg 1200w,
				opera-fullshot-1600.jpg 1600w,
				opera-fullshot-2000.jpg 2000w">
	    <img
		src="opera-fallback.jpg" alt="The Oslo Opera House"
		sizes="(min-width: 640px) 60vw, 100vw"
		srcset="opera-closeup-200.jpg 200w,
				opera-closeup-400.jpg 400w,
				opera-closeup-800.jpg 800w,
				opera-closeup-1200.jpg 1200w,
				opera-closeup-1600.jpg 1600w,
				opera-closeup-2000.jpg 2000w">
    </picture>

### Perch template

<picture>
	<source
		media="(min-width: 1280px)"
		sizes="50vw"
		srcset="<perch:content type="image" id="image" label="Image" width="200" /> 200w,
				<perch:content type="image" id="image" label="Image" width="400" /> 400w,
				<perch:content type="image" id="image" label="Image" width="800" /> 800w,
				<perch:content type="image" id="image" label="Image" width="1200" /> 1200w,
				<perch:content type="image" id="image" label="Image" width="1600" /> 1600w,
				<perch:content type="image" id="image" label="Image" width="2000" /> 2000w">
	    <img
		src="<perch:content type="image" id="image" label="Image" help="Full size image for large screens" />" alt="<perch:content type="text" id="alt" label="Description" required="true" help="Description of subject of these images." title="true" />"
		sizes="(min-width: 640px) 60vw, 100vw"
		srcset="<perch:content type="image" id="imagecloseup" label="Closeup image" help="Closeup image for small screens." width="200" /> 200w,
				<perch:content type="image" id="imagecloseup" label="Closeup image" width="400" /> 400w,
				<perch:content type="image" id="imagecloseup" label="Closeup image" width="800" /> 800w,
				<perch:content type="image" id="imagecloseup" label="Closeup image" width="1200" /> 1200w,
				<perch:content type="image" id="imagecloseup" label="Closeup image" width="1600" /> 1600w,
				<perch:content type="image" id="imagecloseup" label="Closeup image" width="2000" /> 2000w">
    </picture>

