Created by: Rachel Andrew
Created date: 2012-05-31
Last updated: 2014-03-11
Authors: Rachel Andrew, Drew McLellan
Title: How do I get started with PHP?
Tags: PHP

# How do I get started with PHP?

## Perch doesn't require that you know PHP, but with just a little bit of knowledge you will find you can do far more advanced things. This solution gets you started.

You don’t need to know any PHP to use Perch, for basic content all of your customizations happen in your templates which are just HTML snippets.

However, if you want to work with `perch_content_custom()` or do more complex things with apps knowing a little PHP will make your job much easier. If you have learned HTML and CSS then you will not find basic PHP hard at all.

## Important concepts

Unlike HTML and CSS PHP is parsed by the server before it gets to your web browser. This is why – if PHP is running on your server – when you View Source you will not see any of the PHP tags that you entered. There is also no concept of browser compatibility when it comes to serverside scripting like PHP. The browser gets HTML as it would if you had hand-coded the site, it doesn’t know or care that the HTML has been generated using PHP.

In the case of Perch we use PHP to compile together your templates, and the content added to the database by an editor to produce the final page.

In general a server will be configured to parse PHP on any page that has a `.php` extension. Most hosts will allow you to also parse pages with a `.html` extension but you may have to configure this using a `.htaccess` file as we explain in the documentation. If a page is not being parsed as PHP you will see the PHP tags when you View Source.

## How does the server know something is PHP?

When using Perch you add PHP to your page to include Perch and also when creating a Perch Editable Region. In each case you use PHP tags to demonstrate to the server that this is PHP, parse it.

`<?php include('perch/runtime.php'); ?>`

The above line includes the Perch runtime. The PHP tags are the `<?php ?>` everything inside is an instruction for PHP. In this case we are telling PHP to include a file at that location.

Therefore if any documentation tells you to add some PHP to your page, you know it needs to be inside `<?php ?>` otherwise the server doesn’t know to parse it and it will be output as text on your page.

## Variables in PHP

A variable is a value that might change. In PHP variables begin with a dollar sign `$` – a simple use of variables might be to get the value from the QueryString in order to pass it into a function. For example:

    <?php
    //get the value of id from the QueryString
    $id = $_GET['id'];
    //pass it into the perch_blog_post function
    perch_blog_post($id);
    ?>

## Arrays in PHP

Most of our Perch functions take a special kind of variable called an array. An array is simply a list of things stored in a manner that PHP can look through and use.

A simple array looks like this:

    <?php
    $my_shopping = array('eggs','apples','a nice cup of tea');
    ?>

If a variable is an array you can have a look at it by using the PHP `print_r` function. This is very useful if you need to know what an array contains. If I print_r the above array like so:

    <?php
    print_r($my_shopping);
    ?>

In the browser I will see:

    Array ( [0] => eggs [1] => apples [2] => a nice cup of tea )

In Perch we most often use a named array, in the simple array above to use any value you have to know the index of that value – this means you have to create your array in a fixed order to be able to use certain values.

With a named array we essentially have a set of variables contained in a variable, which is very useful and so is how we tend to do things with Perch.

The below array is the options array that you might pass into `perch_content_custom()`.

    <?php
    $opts = array(
        'page'=>'/news/index.php',
        'template'=>'article.html',
        'sort'=>'date',
        'sort-order'=>'DESC',
        'count'=>1
    );
    ?>

The variable that contains the array is called `$opts` we then create an array, but instead of having a comma separated list of things, we have `name => value` pairs.

Each pair has the name first, then the `=>`, then the value. Each line except the last has a comma. It’s just a comma separated list except containing names and values.

All this array says is that:

* the variable ‘page’ has the value ‘/news/index.php’
* the variable ‘template’ has the value ‘article.html’
* we want to ‘sort’ by ‘date’
* we want our ‘sort-order’ to be ‘DESC’ (descending)
* we want the ‘count’ to be ‘1’ – retrieve one item only.

You don’t need to call the array `$opts` – it can be anything you like, it is just a reference, as the next thing you would do is pass this array into the `perch_content_custom()` function.

    <?php 
    $opts = array(
        'page'=>'/news/index.php',
        'template'=>'article.html',
        'sort'=>'date',
        'sort-order'=>'DESC',
        'count'=>1
    );
    perch_content_custom('News', $opts); 
    ?>

In fact you could do this without creating the array as a variable first at all, you can just create the array inside the `perch_content_custom()` function, which may look more of a familiar syntax if you are used to using jQuery for example.

    <?php 
    perch_content_custom('News',  array(
        'page'=>'/news/index.php',
        'template'=>'article.html',
        'sort'=>'date',
        'sort-order'=>'DESC',
        'count'=>1
    )); 
    ?>

## PHP Errors

Sometimes something will go wrong and PHP will throw an error.

When you are working locally, on your own machine, you can get PHP to display errors directly on the screen so you can see them in the browser. How PHP reports errors is configured in a file called php.ini, if you are using XAMPP you can get to this via your control panel by clicking the Config button on the Apache line of buttons and selecting php.ini.

Search for: `display_errors` and make sure that is set to On:

    display_errors = On

Also check that the value of error_reporting is as below, to make sure you get to see all potential errors:

    error_reporting = E_ALL | E_STRICT

On a live server you want errors to not be shown to the screen as they could reveal information that could be a security risk.

When errors are not being shown this will usually mean that a PHP error will cause a “white screen” with nothing showing or a partial load of the document where if you View Source you can see the document stops loading at the point at which PHP threw the error. In this case errors should be logged to a file. You may find this is already available to you in your hosting control panel or in your site via FTP, if not have a look at an article written by Perch developer Rachel Andrew for Smashing Magazine, it details [how to get PHP errors logging on your server](http://coding.smashingmagazine.com/2011/11/30/a-guide-to-php-error-messages-for-designers/).