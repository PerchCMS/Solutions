Created by: Rachel Andrew
Created date: 2014-11-24
Last updated: 2014-11-24
Authors: Rachel Andrew
Title: Using Page Attributes to add Facebook Open Graph Tags and Twitter Cards
Tags: Facebook, twitter, open graph, social

# Using Page Attributes to add Facebook Open Graph Tags and Twitter Cards

## The Page Attributes functionality in Perch makes it simple for you to control how your content looks when it is shared on Twitter and Facebook. This solution shows you how.

Both Twitter and Facebook support open graph tags. These tags go into the head of your document along with other meta information. They allow you to specify a title, description, image and other information that is shown alongside your post on these sites.

If you have ever shared a blog post and then found the Facebook was displaying a strange image picked from your site alongside it, this solution shows you how to fix that problem!

This solution relies on functionality that was released in Perch and Perch Runway 2.7.4 so check that you are running at least that version before continuing.

Perch ships with a basic Page Attributes template that you can find in `perch/templates/pages/attributes`. The default.html template includes seo.html - a template for adding page meta data. To add Facebook and Twitter tags I am going to create two new templates:

* facebook.html
* twitter.html

I then link these into the default.html template.

    <perch:template path="pages/attributes/seo.html" />
    <perch:template path="pages/attributes/facebook.html" />
    <perch:template path="pages/attributes/twitter.html" />

### facebook.html

The contents of this template is as follows:

    <meta property="og:site_name" content="<perch:pages id="sitename" type="hidden" />" />
    <meta property="og:url" content="<perch:pages id="url" type="hidden" />" />
    <meta property="og:title" content="<perch:pages id="og_title" label="Social title" type="text" escape="true" help="Title for this document with no branding or site name" divider-before="Facebook Open Graph Tags" />" />
    <meta property="og:description" content="<perch:pages id="og_description" label="Social description" type="textarea" size="s" escape="true" />" />
    <perch:if exists="og_image">
    <meta property="og:image" content="<perch:pages id="domain" type="hidden" /><perch:pages id="og_image" label="Image when shared" help="Should be at least 1200x630" type="image" width="1200" />" />
    <perch:else />
    <meta property="og:image" content="<perch:pages id="domain" type="hidden" /><perch:pages id="sharing_image" type="hidden" />" />
    </perch:if>
    <perch:if exists="og_type">
    <meta property="og:type" content="<perch:pages id="og_type" label="Facebook type" type="select" options="article,book,profile,website,video,music" allowempty="true" />" />
    </perch:if>
    <perch:if exists="og_author">
    <meta property="article:author" content="<perch:pages id="og_author" type="hidden" />" />
    </perch:if>

* **og:site_name** - this is the name of the site. 
* **og:url** - the page URL
* **og:title** - a title as used on Facebook
* **og:description** - a description
* **og:image** - an image
* **og:type** - a defined type, if not set will default to website
* **og:author** - The author of the piece, needs to be a Facebook Page or Profile.

The Open Graph tags are [detailed on Facebook](https://developers.facebook.com/docs/sharing/best-practices#tags). You can add any other tags that are relevant to your content, in the same way as my examples.

Some of the fields in my template are regular Perch Content tags that will add fields to the Page Details Tab in the Perch Control Panel.

Others have been set to `type="hidden"` because I am going to pass the information to these tags from the page rather than ask an editor to fill them in.

### twitter.html

My twitter.html template contains the following tags.

    <meta name="twitter:card" content="summary" />
    <meta name="twitter:site" content="<perch:pages id="twittername" type="hidden" />" />
    <meta name="twitter:title" content="<perch:pages id="og_title" label="Social title" type="text" escape="true" help="Title for this document with no branding or site name" />" />
    <meta name="twitter:description" content="<perch:pages id="og_description" label="Social description" type="textarea" size="s" escape="true" />" />
    <perch:if exists="og_image">
    <meta property="twitter:image" content="<perch:pages id="domain" type="hidden" /><perch:pages id="og_image" label="Image when shared" help="Should be at least 1200x630" type="image" width="1200" />" />
    </perch:if>
    <meta name="twitter:url" content="<perch:pages id="url" type="hidden" />" />

* **twitter:card** - set to summary, there are other types of card if you are publishing certain content
* **twitter:site** - set to the Twitter handle for the site author
* **twitter:title** - I use the same ID as in the Facebook template so that the editor can enter this once and the content is used for Twitter and Facebook. Change the ID if you want to add special content for each.
* **twitter:image** - reusing the ID for the Facebook image
* **twitter:url** - the URL of the content

You can see the information about these tags on the [Twitter developer site](https://dev.twitter.com/cards/types/summary). As with the Facebook template some of these tags will create a field to complete and others we will pass in values from the page.

### Adding the tags to our pages

In a Perch Layout (or just on each page if you are not using layouts) you can set variables that are then available to the template engine using PerchSystem::set_var. Before including my attribute templates I set these variables. I am getting the domain and full URL of the page, setting the name of the website and including a default image which can be overridden if the content editor uploads a specific one for any page.

Finally I call in my default.html template, which includes my Facebook and Twitter templates. The below code should go in-between the `<head></head>` tags in your page or layout.

    <?php 
    $domain        = 'http://'.$_SERVER["HTTP_HOST"];
    $url           = $domain.$_SERVER["REQUEST_URI"];
    $sitename      = "The name of my website";
    $twittername   = "@mytwittername";
    $sharing_image = '/images/default_fb_image.jpg';
    
    PerchSystem::set_var('domain',$domain);
    PerchSystem::set_var('url',$url);
    PerchSystem::set_var('sharing_image',$sharing_image);
    PerchSystem::set_var('twittername',$twittername);

    perch_page_attributes(array(        
      'template' => 'default.html'    
    ));
    ?>

You should now be able to edit the contents of the template tags in the Page Details section of any page and see the values appear in the head section of your page.

If you are using the Twitter tags you should [validate your card on Twitter](https://cards-dev.twitter.com/validator). This page will also tell you if you need to authorise the use of cards on your domain and allow you to do that.

[Facebook also have a handy tool](https://developers.facebook.com/tools/debug/) that lets you see what will be returned for any URL.

### Pushing blog or other app content into Page Attributes

The above all works well for regular page content, and you can now make sure that each page has the meta information added. However for app content such as blog, or any List/Detail type display of content you may have a single "page" that actually holds the content for 100s of articles.

In Perch 2.7.4 the `perch_page_attributes_extend` function accepts an array of data that will essentially overwrite anything that has been set for the attributes named. Use the function before your layout, or wherever you include your attributes template.

In the following example, I have a post.php that is the page on which blog posts display (this would be the blog post Master Page in Perch Runway).

I get my post using `perch_blog_post_custom` with the `return-html` value set to true. This will give me the full templated blog post but also all the individual fields inside $post[0].

I have added a field to my blog template with an ID of fbimage specifically so that content editors can include an image for social sharing.
    
    <?php
    # get the post
    $post = perch_blog_custom(array(
          'filter'        => 'postSlug',
          'match'         => 'eq',
          'value'         => perch_get('s'),
          'skip-template' => 'true',
          'return-html'   => 'true',
	  ));
    
    # set up the variables
    $title       = $post['0']['postTitle'];
    $description = strip_tags($post['0']['excerpt']);
    $url         = $post[0]['postURL'];
    if (isset($post[0]['fbimage'])) {
	    $fbimage = $post[0]['fbimage'];
    } else {
	    $fbimage = '';
    }
   
    # use the variables in the array value 
    perch_page_attributes_extend(array(
        'description'    => $description,
        'og_description' => $description,
        'og_title'       => $title,
        'og_type'        => 'article',
        'og_image'       => $fbimage,
        'og_author'      => 'https://www.facebook.com/myfbname',
    ));
    ?>

To actually display the blog post, I can save another PHP function call by just echoing out the variable `$post['html']`.

    <?php echo $post['html']; ?>

This process would work for any of the apps, for example pushing in details about a podcast or event. It would also work in a List Detail using perch_content_custom or with Collections in Runway.
