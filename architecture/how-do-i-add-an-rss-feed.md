# How do I add an RSS feed to a news page?

## In this article we’ll look at how to use the power of perch_content_custom() and templates to create a simple RSS feed for content stored in a standard multiple item region in Perch.

In this article we’ll look at how to use the power of `perch_content_custom()` and templates to create a simple RSS feed for your site.

To do this, we’ll assume that you already have a multiple-item region set up with the content that you want to replicate in the RSS feed. For us, that’s going to be a region called ‘News’ on the page /news.php – just adapt the examples accordingly to fit your own site.

The solution is more straightforward than you might think. RSS feeds are a form of XML, which is a text format based on tags just like HTML. We’re going to create a page using XML tags instead of HTML, and pull in the content from the News page using perch_content_custom().

## Creating the page

First we need to add a new page to our site. I’m calling mine rss.php and placing it at the top level alongside my news.php page. RSS feeds are made up of two main parts. The first is general information about the feed (the title etc, similar in many ways to the <head> section of an HTML page) and then the news items themselves.

    <?php include('perch/runtime.php'); ?>
    <?php echo '<'.'?xml version="1.0"?'.'>'; ?>
    <rss version="2.0">
    <channel>
        <title>Example Co News</title>
        <link>http://example.com/news.php</link>
        <description>News and information about Example Co</description>
    </channel>
    </rss>

The first line is the familiar Perch runtime link. The strange incantation on the second line is a workaround necessary for using the XML `<?xml ... ?>` prolog on PHP servers which mistake this for a PHP opening tag. It’s strange, but copy it as written and it should be fine.

Next we have the basic structure of the RSS feed. Go ahead and set the title, link and description to be whatever you need for your site. You could even make these editable using perch_content() regions.

So that’s the basic outline of the feed. Next we need to make a template to use in a repeating region for the news items.

## Creating the template

Add a new file for your template in perch/templates/content/. I’m calling mine _rss_item.html. Starting the file name with an underscore causes it to be hidden from the web interface, as this isn’t a template we need available for regular regions.

    <item>
    <title></title>
    <link></link>
    <description>
        <![CDATA[
        
        ]]>
    </description>
    </item>

Again, the basic outline for an item is quite simple. The only strange thing here is the CDATA block inside the <description> tags – that’s required if we want to put HTML inside the item.

Next we need to add the perch:content tags to our template, using the same id attributes as appear in the template that our main news items use. For me, that’s article.html.

    <item>
    <title><perch:content id="heading" type="text" label="Heading" /></title>
    <link>http://example.com/news.php#news<perch:content id="perch_item_index" type="hidden" /></link>
    <description>
        <![CDATA[
            <perch:content id="body" type="textarea" label="Body" textile="true" />
        ]]>
    </description>
    </item>

If you want to use just an excerpt in your feed, you can use the [words attribute](http://docs.grabaperch.com/docs/templates/attributes/words/) to limit the number of words you output.

Worth noting here is the way the content for the <link> tag is created. We’re using the perch_item_index special value to create a link to the item on our news page. To make this work, I’ve added the same to the article template:

    <h2 id="news<perch:content id="perch_item_index" type="hidden" />">...</h2>

Obviously, you’ll also want to update the http://example.com/news.php to be the correct URL of your news page.

## Putting the two together

So we have our RSS page, and we have a template to display the items. We just need to put the two together. The items appear after the <description> tags in an RSS feed.

<?php include('perch/runtime.php'); ?>
<?php echo '<'.'?xml version="1.0"?'.'>'; ?>
<rss version="2.0">
    <channel>
        <title>Example Co News</title>
        <link>http://example.com/news.php</link>
        <description>News and information about Example Co</description>
        <?php
            $opts = array(
                    'page'=>'/news.php',
                    'template'=>'_rss_item.html'
                );
            perch_content_custom('News', $opts);
        ?>
    </channel>
</rss>

We set the options for perch_content_custom() to take the content from the page our news is on, and tell it to use the template we created for the RSS items. We then use the same region name that our news page uses.

## Linking the feed to the news page

RSS feeds are included using a <link> tag in the <head> of a page. This is how you get the feed to show up as an RSS icon in the browser’s location bar. Add the following to the <head> section of your news page:

<link rel="alternate" type="application/rss+xml" title="RSS" href="/rss.php" />

And that’s it – we’re done.