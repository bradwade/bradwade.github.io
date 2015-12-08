---
layout: article
title: Override Core CSS in Drupal 8 Themes
categories: drupal8
comments: true
share: true
image:
  teaser: triboro-800-500.jpg
  feature: triboro-1140-285.jpg
  credit: Joshua Brandenburg
  creditlink: http://www.drinkandsmile.com/
excerpt: Overriding Drupal core CSS in your theme by modifying core library definitions.

---

Previously in Drupal 8 beta versions, it was possible in your .info.yml file to specify core css files for which you had an alternate version in your theme.Doing this would not use the core version and use your theme's version instead. This is no longer possible. To replicate this behavior, we now need to do this manually in our .theme file by using hook_library_info_alter().

## Using hook_library_info_alter()

{% highlight php startinline=true %}
/**
 * Implements hook_library_info_alter().
 */
function THEMENAME_library_info_alter(&$libraries) {
  if (isset($libraries['base'])) {
    unset($libraries['base']['css']['theme']['css/system.theme.css']);
    $libraries['base']['dependencies'][] = 'THEMENAME/NAMESPACE.LIBRARYNAME';
  }
}
{% endhighlight %}

So we unset the declaration of the css file in the core library, then add to the core library a dependency on a custom library in our theme.

Then in our theme's .libraries.yml file declare the custom library with the alternate css file.

{% highlight yaml startinline=true %}
NAMESPACE.LIBRARYNAME:
  css:
    theme:
      css/system.theme.css: { every_page: true, weight: -10 }
{% endhighlight %}

## Alternative Approach: Remove the Core CSS File

To achieve more or less the same outcome with less code, you can simply remove system css in your .info.yml file. Then add a file with the alternative CSS in your own custom css file.

In .info.yml file:

{% highlight yaml startinline=true %}
stylesheets-remove:
  - normalize.css
{% endhighlight %}

While valid for now, I would consider this deprecated as plans are to remove this in the future.

## Other uses for modifying core libraries

Although it may not be necessary in this use case, knowing how to access and modify/remove aspects of all of Drupal libraries at the theme layer is a powerful technique. Examine $libraries variable inside of hook_library_info_alter() to see all the possible modifications you can make.

For more information see 
[my post all about including JS and CSS in your Drupal 8theme using libraries.]({% post_url drupal8/2015-11-27-D8-3-Libraries %})
