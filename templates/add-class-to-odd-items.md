Created by: Rachel Andrew
Created date: 2014-03-12
Last updated: 2014-03-12
Authors: Rachel Andrew
Title: How do I add a class to every other item?
Tags: templates

# How do I add a class to every other item?

## You want to add a class to every other item in Perch so you can style it using CSS.

You can use the [perch:every](http://docs.grabaperch.com/docs/templates/conditionals/every/) tag to achieve this.

    <li<perch:every count="2"> class="odd"</perch:every>> ... </li>

While needing to add classes for presentational purposes is becoming less of a requirement as more browsers support CSS3 selectors such as `nth-child`, it is worth remembering that you could use this technique to include additional markup or anything else you want to do with alternate items.