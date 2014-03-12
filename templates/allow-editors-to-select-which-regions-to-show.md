Created by: Rachel Andrew
Created date: 2014-03-12
Last updated: 2014-03-12
Authors: Rachel Andrew
Title: How do I let my editor select which items to display in a multiple-item region?
Tags: templates, multiple-item region

# How do I let me editor select which items to display in a multiple-item region?

## You want your editors to be able to create a list of content and use a checkbox to display certain ones on the site.

The first step is to add a checkbox to your template. This will enable your editor to make their selection. 

    <perch:content id="showprofile" type="checkbox" label="Display on site" value="1" suppress="true" />

The suppress="true" attribute ensures that this does not output a `1` to your site when checked.

We can now test to see if the value of show profile is 1 using `perch:if`.

    <perch:if id="showprofile" value="1">
      <h3>
		    <perch:content id="firstname" type="text" label="First name" required="true" title="true" order="1" />
		    <perch:content id="lastname" type="text" label="Last name" required="true" title="true" order="2" />
	    </h3>
	    <p class="job-title">
		    <perch:content id="jobtitle" type="text" label="Job title" order="3" />
	    </p>
		  <perch:content id="showprofile" type="checkbox" label="Display on site" value="1" suppress="true" />
    </perch:if>