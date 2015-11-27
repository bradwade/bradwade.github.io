---
layout: article
title: Disable CSS Aggregation for Specific CSS files in Drupal 8
categories: drupal8
comments: true
share: true
image:
  teaser: triboro-800-500.jpg
  feature: triboro-1140-285.jpg
  credit: Joshua Brandenburg
  creditlink: http://www.drinkandsmile.com/
excerpt: How to disable CSS aggregation for individual CSS files.

---

### How to Force Drupal to NOT aggregate specific CSS files.

Generally we want to aggregate all our CSS into one file. This is how Drupal libraries work by default. However, there are some use cases when you will need to NOT aggregate some specific CSS files, while aggregating all of the rest.

This will need to be done, for example, for any file that is intentionally breaking itself up into multiple, smaller files by using multiple imports to work around IE CSS selector limits. See http://blesscss.com/.

When creating a library in Drupal, set "preprocess" to false for that specific CSS file. 

{% highlight yaml %}
    msk.globalstyles:
   css:
     theme:
       assets/styles/legacy.css: { browsers: { IE: 'lt IE 9', '!IE': false }, preprocess: FALSE }
{% endhighlight %}

For more information see 
[my post all about including JS and CSS in your Drupal 8theme using libraries.]({% post_url drupal8/2015-11-27-D8-3-Libraries %})
