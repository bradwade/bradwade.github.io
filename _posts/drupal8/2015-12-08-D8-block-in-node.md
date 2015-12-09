---
layout: article
title: Placing a block in a node
categories: drupal8
comments: true
share: true
image:
  teaser: triboro-800-500.jpg
  feature: triboro-1140-285.jpg
  credit: Joshua Brandenburg
  creditlink: http://www.drinkandsmile.com/
excerpt: Generally in a Drupal 8 theme, blocks can be placed in regions which are placed in a page.html.twig template. How do you display a block inside a node template?
---
Generally in a Drupal 8 theme, blocks can be placed in regions which are placed in a page template. How do you display a block inside a node template?

Prerequisite: Create the block and place an instance of it in a region or in the 'disabled' region.

While preprocessing the node in your THEMENAME.theme file...

{% highlight php startinline=true %}
function mskcc_preprocess_node(&$variables) {      
  /* Create variable that contains breadcrumb for node templates. */

  /* create a block object */
  $my_block_object = \Drupal\block\Entity\Block::load('breadcrumb');

  /* creates a renderable array from the block object */
  $variables['breadcrumb_in_node'] = \Drupal::entityManager()->getViewBuilder('block')->view($my_block_object);
}
{% endhighlight %}
      
The block can now be printed by placing \{\{ breadcrumb_in_node \}\} wherever you like in a twig node template.
