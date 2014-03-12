Created by: Rachel Andrew
Created date: 2014-03-12
Last updated: 2014-03-12
Authors: Rachel Andrew
Title: How do I display a random item from a multiple-item region?
Tags: templates, perch_content_custom

# How do I display a random item from a multiple-item region?

## You have a multiple-item region and would like to display one item at random from it, perhaps on your homepage.

You can select from content used elsewhere on your site with `perch_content_custom`. To display the content randomly use a sort-order of `RAND`, to display only one item set count to 1.

    <?php perch_content_custom('Testimonials',array(
      'page' => '/testimonials.php',
      'template' => '_home_testimonial.html',
      'sort' => 'familyname',
      'sort-order' => 'RAND',
      'count' => 2
    ));

You can also see this solution in our video tutorial on [using perch_content_custom](http://docs.grabaperch.com/video/tutorials/swift/using-perch-content-custom/).