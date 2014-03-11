Created by: Rachel Andrew
Created date: 2012-05-31
Last updated: 2014-03-11
Authors: Rachel Andrew, Drew McLellan
Title: How do I create a FAQ?
Tags: perch_content_custom

# How do I create a FAQ?

## An FAQ page often has a list of links at the top, skipping down to the answers below. This solution demonstrates how to create this in Perch.

In this tutorial we will create an example FAQ page using a custom template. We will also use perch_content_custom to create a list of links at the top of the page jumping down to the individual FAQ answers.

The first thing we need to do is to create our FAQ template. The quickest way to do that is to look in the perch/templates/content directory and grab one of the example templates as a starting point. I’m going to use article.html.

Open article.html in a text editor save it as faq.html and delete everything other than the heading and body tags.

I am also going to change the Heading tag to be named Question and Body to Answer just to make it clear to editors what needs to be entered here and, as this will be a list of FAQ questions and answers, I’ve wrapped the items in an li element.

The final code for this template is shown below. Save the template.

    <li>
      <h2><perch:content id="question" type="text" label="Question" required="true" /></h2>
      <perch:content id="answer" type="textarea" label="Answer" textile="true" editor="markitup" required="true" />
    </li>

Now go back to your FAQ page. We just need to add Perch to this page.

Add the include for the Perch runtime at the top of the document and then add a Perch Region to create a content area for the FAQ. I have surrounded this call with an unordered list to wrap the list items in the FAQ template that I created in the last step.

    <ul class="faq">
      <?php perch_content('FAQ'); ?>
    </ul>

You are ready to start adding FAQ items. Refresh your FAQ page so that Perch picks up the new region, then log into the administration area. You should see that your FAQ page is now showing as having new content.

Click on the page name, then on the FAQ Reqion within that page.

Select FAQ from the dropdown list for template. As you will want the user to be able to add multiple FAQ items, check the allow multiple checkbox and submit the form.

The page will reload and you will be able to add your first FAQ item. After adding the item click the “Save, and add another” button to add another item.

If you have a lot of items you may want to switch this region into List/Detail View. Just visit the Region Options and uncheck ‘Edit all on one page’ to enable this.

After adding your items refresh the FAQ page on your site to view the content.

## Adding a list of links to individual FAQ items

The above process might be all you need for your FAQ page, however on a long page you might like to have a list of the questions at the top of the page and use an anchor to jump to individual answers. You achieve this in Perch by using the perch_content_custom tag.

The perch_content_custom tag is really useful if you want to reuse content from one page on another (for example showing 2 items from your news page on the homepage) it can also be used to create an anchor list for our FAQ page.

Above your FAQ list add the following code:

    <ul class="questions">
    <?php
      perch_content_custom('FAQ', array(
        'template'=>'faq_question.html',
        'page'=>'/faq.php'
      ));
    ?>
    </ul>

We are opening an unordered list for the links.

Then we call perch_content_custom passing in the ID of the area on the page our content should come from, which is ‘FAQ’, and an array of options.

In this case our options are quite simple:

* template is set to faq_question.html, we will create this template next
* page is set to /faq.php this is my FAQ page in my site

Now create a new template in the perch/templates/content directory with a single list item of the question. Wrap the question in a link.

To create our anchors in the link we can use the perch_item_index tag, which will give you the unique index of that content item. This is ideal for creating our anchor links by adding the unique id onto the end of the word faq, creating an ID of faq1, faq2 and so on.

    <li>
      <a href="#faq<perch:content id="perch_item_index" type="hidden" />">
        <perch:content id="question" type="text" label="Question" required="true" />
      </a>
    </li>

Now open the initial faq.html template that you created and add an ID to the h2 element, the ID value will be the word faq plus the item index. The attribute type needs to have a value of hidden to stop this showing up as an editable field in the admin.

    <li>
      <h2 id="faq<perch:content id="perch_item_index" type="hidden" />">
        <perch:content id="question" type="text" label="Question" required="true" />
      </h2>

      <perch:content id="answer" type="textarea" label="Answer" textile="true" editor="markitup" required="true" />
    </li>

To get your content to pick up the template changes you will need to visit the page in the admin and edit and save the FAQ region. After doing this refresh your page and you should see that you have a list of FAQ questions at the top of the page, clicking on any question will jump down to the FAQ answer.