Created by: Rachel Andrew
Created date: 2014-03-12
Last updated: 2014-03-12
Authors: Rachel Andrew
Title: How do I only show a section of a template if content has been entered?
Tags: templates, conditionals

# How do I only show a section of a template if content has been entered?

## If parts of your template are not required you may need to exclude some HTML output.

You can use the [perch:if](http://docs.grabaperch.com/docs/templates/conditionals/if/) tag to check to see if content has been entered. In the below example I am using `perch:if` to test to see if an image has been uploaded. I only display the mark-up for the figure if one has.

     <perch:if exists="figure">
		   <figure>
         <img src="<perch:content id="figure" type="image" label="Upload a figure" width="640" height="480"/>" alt="<perch:content id="alt" type="text" label="Alt text" />" />
        
         	<figcaption><perch:content id="caption" type="text" label="Figure caption" /></figcaption>
       	</figure>
      </perch:if>

## Second Example

A second optimization can be made by adding a nested if statement. In this example, mark-up for figcaption only displays if there is a caption.


		<perch:if exists="figure">
			<figure>
		 		<img src="<perch:content id="figure" type="image" label="Upload a figure" width="640" height="480"/>" alt="<perch:content id="alt" type="text" label="Alt text" />" />
			  <perch:if exists="caption">
			  <figcaption><perch:content id="caption" type="text" label="Figure caption" /></figcaption>
			  </perch:if>
			</figure>
		</perch:if>


