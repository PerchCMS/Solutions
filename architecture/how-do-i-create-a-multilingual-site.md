Created by: Drew McLellan
Created date: 2014-03-11
Last updated: 2014-03-11
Authors: Drew McLellan
Title: How do I create a multi-lingual website?
Tags: multilingual

# How do I Create a Multi-lingual Website?

## This solution outlines your options for creating a site in more than one language using Perch.

Although Perch is a deliberately simple CMS and as such doesn’t have native multilingual website functionality, it is flexible enough to enable you to implement a basic multilingual site yourself.

There are two common strategies to approaching this, and we’ll look at both below.

## Strategy one: a branched site

Probably the most common approach to creating a multilingual site is to branch your site at the top level and have different folders for each language option.

* http://mysite.com/ would be a simple splash screen asking visitors to choose a language (which would simply be links to…)
* http://mysite.com/en would be the home page for the English version of the site
* http://mysite.com/fr would be the home page for the French version of the site, and so on.

You would then build out your pages as normal. This offers a lot of flexibility to present your content differently for different audiences, and enables you to localize your site, not just translate it.

## Strategy two: a region for each language

If you don’t wish to maintain separate pages for each language choice, another option is to duplicate each region, once for each language.

Suppose we have a PHP variable called $lang which contains a language choice. This would be something like en for English or de for German. If we create our regions with the language choice added onto the region name, we can get a copy of each region for each language option:

    <?php perch_content('Main heading - '.$lang); ?>

When the language is set to en for English, this would create a region called Main heading – en and for German it would be Main heading – de. When editing the content in Perch, you then just pick the region for the language you want to work on.

So how do we set $lang to be our language choice? Add this snippet to the top of each page (or better still, put it in an include and add that to the top of each page).

    <?php
    session_start();
    if (isset($_GET['lang']) && $_GET['lang']!='') {
        $lang = $_GET['lang'];
        $_SESSION['lang'] = $lang;
    }elseif (isset($_SESSION['lang'])){
        $lang = $_SESSION['lang'];
    }else{
        // default language
        $lang = 'en';
    }
?>

The first thing to know is that we’re setting the default language to en – so if no other choice is made, the site will be in English. You can change that where commented at the bottom of the snippet.

The logic of the code goes like this:

* Is there a lang option set on the URL? If so, use that, and store it in the session for next time.
* If not, is there a lang option stored in the user’s session? If so, use that. Otherwise, use English.

To switch language, you just need to make a link on your page such as:

    /index.php?lang=de

This will cause the page to load the German regions, and store that choice for future pages. So unless you’re actually switching language, you don’t need to add anything special to your links.