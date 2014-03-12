Created by: Rachel Andrew
Created date: 2014-03-12
Last updated: 2014-03-12
Authors: Rachel Andrew
Title: How do I show a placeholder if no image is uploaded?
Tags: templates, images

# How do I show a placeholder if no image is uploaded?

## If the content editor has uploaded an image we want to display it. If they have not we will display a placeholder.

We combine perch:if and perch:else to achieve this. First we use `perch:if` and check to see if an image has been uploaded. We then use `perch:else` to say what to do if we don't have an image.

    <perch:if exists="image">
		  <perch:content id="image" type="image" label="Avatar" width="80" height="80" crop="true" output="tag" />
	  <perch:else />
		  <img src="/img/placeholder-avatar.png" alt="" />
	  </perch:if>