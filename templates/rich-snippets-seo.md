Created by: Rachel Andrew
Created date: 2014-08-05
Last updated: 2014-08-05
Authors: Rachel Andrew
Title: How do I use rich snippets for SEO in Perch
Tags: seo, google, rich snippets, microdata

# How do I use rich snippets for SEO in Perch?

## You would like to add rich snippets to your content to improve how your data is displayed in search engine result pages.

Google and other search engines support [Rich Snippets](https://support.google.com/webmasters/answer/99170?hl=en), a way to indicate to the search engine that certain content is special. These snippets are then used on search engine result pages. Perch is ideal for ensuring that your content is correctly marked up to take advantage of this.

Google suggests using Microdata to create your rich snippets and supports the following content types:

* Reviews
* People
* Products
* Businesses and Organizations
* Recipes
* Events
* Music

The below templates are examples, based on those shown on Google, including help text to ensure that content editors enter the correct content.

It is worth noting that while you need to ensure that the microdata attributes are correct you do not have to use the particular tags - for example span or div, or a certain heading level. Those can be changed to fit your content.

## Reviews

A [review](https://support.google.com/webmasters/answer/146645) can be represented as a single review or as an aggregate.

If you are using this markup the main topic of the page needs to be the item being reviewed, not a list of items. So this would be ideal to add to a product page for example.

### Single Review template

    <div itemscope itemtype="http://data-vocabulary.org/Review">
      <h3 itemprop="itemreviewed"><perch:content id="title" type="text" label="Title" required="true" title="true" help="Must be the name of the product that is being reviewed" /></h3>
      <p>Reviewed by <span itemprop="reviewer"><perch:content id="author" type="text" label="Author" required="true" /></span> on
      <time itemprop="dtreviewed" datetime="<perch:content id="date" type="date" label="Review date" format="Y-m-d" />"><perch:content id="date" type="date" label="Published date" format="F j" /></time>.</p>
      <p itemprop="summary"><perch:content id="summary" type="text" label="Summary" required="true" help="One line summary of the review" /></p>
      <div itemprop="description"><perch:content id="body" type="textarea" label="Review" markdown="true" editor="markitup" required="true" /></div>
      <p>Rating: <span itemprop="rating"><perch:content id="rating" type="text" label="Rating" required="true" help="Rating between 1 and 5, 1 being the lowest" size="s" /></span></p>
    </div>

### Aggregate Review Template

    <div itemscope itemtype="http://data-vocabulary.org/Review-aggregate">
      <h3 itemprop="itemreviewed"><perch:content id="title" type="text" label="Title" required="true" title="true" help="Must be the name of the product that is being reviewed" /></h3>
      <img src="<perch:content type="image" id="image" label="Image" width="800" />" alt="<perch:content id="title" type="text" label="Title" />" />
      <p><span itemprop="rating" itemscope itemtype="http://data-vocabulary.org/Rating">
      <span itemprop="average"><perch:content id="rating" type="text" label="Rating" required="true" help="Average review rating, eg: 9" size="s" /></span>
      out of <span itemprop="best"><perch:content id="ratingbest" type="text" label="Rating top score" required="true" help="The top score a user could select, eg: 10" size="s" /></span>
      </span>
    based on <span itemprop="votes"><perch:content id="numvotes" type="text" label="Number of votes" required="true" help="How many people rated this item?" size="s" /></span> ratings.
      <span itemprop="count"><perch:content id="numreviews" type="text" label="Number of reviews" required="true" help="How many people reviewed this item?" size="s" /></span> user reviews.</p>
    </div> 

## People

You can mark-up a [person](https://support.google.com/webmasters/answer/146646) with a range of properties and even signify relationships. 

### Person template

    <div itemscope itemtype="http://data-vocabulary.org/Person">
      My name is <span itemprop="name"><perch:content id="fullname" type="text" label="Full name" required="true" title="true" /></span>, 
      but people call me <span itemprop="nickname"><perch:content id="nickname" type="text" label="Nickname" /></span>.
      Here is my homepage: 
      <a href="<perch:content id="url" type="text" label="Homepage URL" required="true" />" itemprop="url"><perch:content id="url" type="text" label="Homepage URL" /></a>.
      I live in 
      <span itemprop="address" itemscope
    itemtype="http://data-vocabulary.org/Address">
    <span itemprop="locality"><perch:content id="city" type="text" label="City" required="true" /></span>, 
    <span itemprop="region"><perch:content id="state" type="text" label="State" required="true" /></span> 
      </span>
      and work as an <span itemprop="title"><perch:content id="jobtitle" type="text" label="Job title" required="true" /></span>
      at <span itemprop="affiliation"><perch:content id="company" type="text" label="Employer" required="true" /></span>.

      <perch:repeater id="friends" label="Friends">
      <perch:before>
      <h3>My friends:</h3>
      <ul>
      </perch:before>

        <li><a href="<perch:content id="friendurl" type="text" label="Homepage" />" rel="friend"><perch:content id="friendname" type="text" label="Name" /></a></li>

      <perch:after>
      </ul>
      </perch:after>

      </perch:repeater>

    </div>


## Recipe

The [recipe](https://support.google.com/webmasters/answer/173379) rich snippet is for recipe information and allows you to indicate things about the recipe such as calorie count and preparation time.

### Recipe template

    <div vocab="http://schema.org/" typeof="Recipe">
      <h1 property="name"><perch:content id="title" type="text" label="Recipe title" required="true" /></h1>
      <p>By <span property="author"><perch:content id="author" type="text" label="Author" required="true" /></span>,
  <meta property="datePublished" content="<perch:content id="date" type="date" label="Published date" format="Y-m-d" />"><perch:content id="date" type="date" label="Published date" format="F j, Y" /></p>
      <img property="image" src="<perch:content type="image" label="Image" id="Image" width="800" />" alt="<perch:content id="alt" type="text" label="Image description" />" />
      <div property="description"><perch:content id="description" type="textarea" label="Description" size="s" markdown="true" editor="markitup" required="true" /></div>
      <p>Prep Time: <meta property="prepTime" content="PT<perch:content id="preptime" type="text" label="Prep time" required="true" help="Add the preparation time as a number in minutes" size="s" />M" /><perch:content id="preptime" type="text" label="Prep time" /> minutes
      <br />Cook time: <meta property="cookTime" content="PT<perch:content id="cooktime" type="text" label="Cook time" required="true" help="Add the cooking time as a number in minutes" size="s" />M" /><perch:content id="cooktime" type="text" label="Cook time" /> minutes
     <br />Yield: <span property="recipeYield"><perch:content id="yield" type="text" label="Yield" required="true" help="For example - 1 loaf or 12 buns" size="m" /></span></p>

     <div property="nutrition" typeof="NutritionInformation">
       <h3>Nutrition facts:</h3>
       <p><span property="calories"><perch:content id="calories" type="text" label="Calories" required="true" size="s" /> calories</span>,
       <span property="fatContent"><perch:content id="fat" type="text" label="Fat" required="true" help="Amount of fat in grams" size="s" /> grams fat</span></p>
      </div>
      
	    <perch:repeater id="ingredients" label="Ingredients">
	      <perch:before>
	      <h3>Ingredients:</h3>
	      <ul>
	      </perch:before>
        <li><span property="ingredients"><perch:content id="ingredient" type="text" label="Ingredient" /></span>
        <perch:after>
        </ul>
        </perch:after>
      </perch:repeater>
	  
	    <perch:repeater id="instructions" label="Instructions">
	      <perch:before>
        <h3>Instructions:</h3>
        <ol property="recipeInstructions">
	      </perch:before>
	
        <li><perch:content id="step" type="text" label="Recipe step" /></li>

        <perch:after>
        </ol>
        </perch:after>
        </perch:repeater>
    </div>

## Validating Rich Snippets

Once you have added rich snippets to your site, check that the markup is correct. You can do this by from within Google Webmaster Tools using the [Structured Data Testing Tool](http://www.google.com/webmasters/tools/richsnippets). 

With correctly used rich snippets on your pages you can then look forward to enhanced content in your search engine results.