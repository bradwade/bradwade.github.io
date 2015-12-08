---
layout: article
title: Adding classes to body and html tags
categories: drupal8
comments: true
share: true
image:
  teaser: triboro-800-500.jpg
  feature: triboro-1140-285.jpg
  credit: Joshua Brandenburg
  creditlink: http://www.drinkandsmile.com/
excerpt: In your Drupal 8 theme, you can add classes to the body and html classes via your THEMENAME.theme file.
---
In your Drupal 8 theme, you can add classes to the html and body tags within the preprocess_html function in your .theme file.

{% highlight php startinline=true %}
function THEMENAME_preprocess_html(&$variables) {
  /* Add class to html tag */
  $variables['html_attributes']->addClass('no-js');
  /* Set the section class on the BODY tag. */
  $variables['attributes']['class'][] = 'my__special--class';
}
{% endhighlight %}

Notice, however that the method for adding a class to each one is different. Why?

![dsm of attributes]({{ site.url }}/images/2015-12-07-dsm.png)

If we look at a dsm() of each, you will notice that `$variables['attributes']['class']` at this point is an array of classes, so we can just add a class to that array. `$variables['html_attributes']` however is an object. 

![dsm of attributes with available methods]({{ site.url }}/images/2015-12-07-dsm-available-methods.png)

In the dsm output there a tab for "available methods". In that list you will find the method `addClass()` that we are using here.
