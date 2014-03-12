Created by: Rachel Andrew
Created date: 2014-03-12
Last updated: 2014-03-12
Authors: Rachel Andrew
Title: How do I use my content template includes inside apps?
Tags: templates, reuse

# How do I use my content template includes inside apps?

## If you are using template includes to tidy up your templates you may run into a problem. If you want to use a content template partial inside blog then you need to use perch:blog tags rather than perch:content.

The template include syntax includes a method of rescoping template tags to correct the namespace.

I have a template partial saved as `_figure.html` which looks like this.

    <perch:if exists="figure">
		   <figure>
         <img src="<perch:content id="figure" type="image" label="Upload a figure" width="640" height="480"/>" alt="<perch:content id="alt" type="text" label="Alt text" />" />
         <figcaption><perch:content id="caption" type="text" label="Figure caption" /></figcaption>
       </figure>
	   </perch:if>

I can include it in a content template like this.

    <article>
      <h1><perch:content id="title" type="text" label="Article Title" /></h1>
    <perch:template path="content/_figure.html" />
      <perch:content id="content" type="text area" label="Article Body" />  
    </article>

To use it in blog I just need to use the `rescope` attribute to include it in my post.html template. It will then act as if all `perch:content` tags in the partial start with `perch:blog`.

    <h1><perch:blog id="postTitle" type="text" required="true" size="xl" /></h1>
    <time datetime="<perch:blog id="postDateTime" format="%Y-%m-%d" />" pubdate class="published"><perch:blog id="postDateTime" format="%d %B %Y" /></time>
    
		<perch:template path="content/_figure.html" rescope="parent" />
                
    <div class="description entry-content">
      <perch:blog id="postDescHTML" type="textarea" encode="false" editor="markitup" textile="true" size="xxl" required="true" />
    </div>

