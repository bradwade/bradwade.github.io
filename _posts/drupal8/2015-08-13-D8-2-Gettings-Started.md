---
layout: article
title: 2) Getting Started with a Drupal 8 Theme
subtitle: Lessons from the Road
categories: drupal8
comments: true
share: true
image:
  teaser: triboro-800-500.jpg
  feature: triboro-1140-285.jpg
  credit: Joshua Brandenburg
  creditlink: http://www.drinkandsmile.com/
excerpt: An overview of a Drupal 8 theme's files, folder structure, organization and info file.

---

## Lessons From the Road

{{ site.data.posts-d8-theming.lessons-excerpt }}

{% include toc.html %}

## Overview of files and folders

When you look into Drupal's root folder, there is a new folder there called "themes" wherein your custom theme folder will reside. While the old D7 path (sites/SITENAME/themes/) is still valid location, let's start using the new root level themes folder, as it seems destined to happily be accepted as the best practice. So create a folder with your theme's name and place it inside DRUPAL_ROOT/themes/

The basic files and structure in your theme is as follows:

{% include finder.html finderlist=site.data.posts-d8-theming.finder.basiclist %}

MYTHEME.settings.yml
: default configuration to be used when theme is enabled.

templates directory
: a directory in which you can place your custom twig template files for overriding core templates.

favicon.ico
: default place that Drupal will look for your theme's favicon.

MYTHEME.info.yml
: the basic meta data about your theme (more below)

MYTHEME.libraries.yml
: defines css and js libraries and dependencies that can be included in your theme

MYTHEME.theme
: custom code for your theme including preprocessing, altering template suggestions and more!

screenshot.png
: default place that Drupal will look for a screenshot of your theme which will be used on the admin/appearance page when enabling themes.

Now you are also going to need a place for your custom CSS, javaScript, images, fonts, and other assets. How you organize these in your theme is a bit of personal taste. If you are pulling in these assets from a prototype system such as pattern lab, you may want to have your grunt automation place all of these things into one assets folder organized like so:

{% include finder.html finderlist=site.data.posts-d8-theming.finder.assetlist %}

Or for example if you are developing right in your Drupal theme, with tools such as sass, compass, bundlr, bower, and Grunt you can put your config.rb, Gemfile, Gruntfile.js, etc. right in your theme root.

{% include finder.html finderlist=site.data.posts-d8-theming.finder.biglist %}

However you decide to organize your assets, we will need to let Drupal know where to find things and what to include which I will be covering in a future installment.

## Overview of the info.yml file.

The file called, THEMENAME.info.yml defines the basic meta data about your theme.

Basic .info.yml file

{% highlight yaml %}
name: MYTHEME
type: theme
description: 'A custom theme for MYTHEME'
package: Custom
core: 8.x
base theme: classy
libraries:
  - mskcc/mytheme.globalstyles
  - mskcc/mytheme.globalscripts
regions:
  header: Header
  utility_nav: 'Utility Nav'
  subheader: 'Subheader'
  breadcrumb: 'Breadcrumb'
  content_top: 'Content Top'
  content: Content
  content_bottom: 'Content Bottom'
  content_related: 'Related Content'
  sidebar_first: 'Sidebar first'
  sidebar_second: 'Sidebar Second'
  footer_connect: 'Footer Connect'
  footer_sitemap: 'Footer Sitemap'
  footer_whatsnew: 'Footer Whats New'
  footer_siteinfo: 'Footer Site Info'
  off_canvas: 'Off Canvas'
  debug_messages: Debug Messages

stylesheets-override:
  - css/system.theme.css

stylesheets-remove:
  - normalize.css
{% endhighlight %}


name and description
: as they will appear on appearance page admin/appearance

type
: "theme" for themes (as opposed to "module" for modules)

package
: Name to group things together. For example, core themes use "Core".

core
: drupal version

base theme
: the parent theme being used. If not using any just omit the line altogether.

libraries
: defining which css and JS libraries will be used

regions
: machine_name: 'Friendly Name' of regions in which you can place blocks.

stylesheets-override/stylesheets-remove
: a list of core stylesheets that you would like to override and a list of that you would like to remove.

> A note on base themes:
> A parent theme's preprocessing code, templates, and css are used by default, however the regions defined in a parent theme are not automatically available to the child them, so you need to define the regions again in your theme.

## Quick intro to YAML

YAML is a format that is used to represent serialized data, but does so in a way that makes it more human readable than other options (such as JSON). Ways that it achieves better human readablity is by not using enclosures (such as brackets) or open/close-tags and representing hierarchy via whitespace indentation. Keep in mind that even though it is human readable, it still has a syntax that needs to be learned. [Check out wikipedia for more info...](https://en.wikipedia.org/wiki/YAML)
