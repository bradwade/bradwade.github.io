---
layout: article
title: Getting Started with a Drupal 8 Theme
categories: drupal8
comments: true
share: true
image:
  teaser: nature-q-c-800-500-1.jpg
  feature: nature-q-g-1024-256-5.jpg
  credit: Michael Rose #name of the person or site you want to credit
  creditlink: http://mademistakes.com #url to their site or licensing
---

## Lessons from the road. 

Back in [DATE] I set out on an adventure with Memorial Sloan Kettering and a band of merry Phase2 developers and peeps to begin building the first fully-operational enterprise D8 website. We launched. We were successful. Blah, blah, blah. Over the past year we have learned much. Want to share the real-world secrets we learned to help get everyone comfortable and start adopting Drupal 8.

{% include toc.html %}

## Getting started with a new D8 theme  

### Overview of files and folders

When you look into Drupal's root folder, there is a new folder there called "themes" wherein your custom theme folder will reside. While the old D7 path (sites/SITENAME/themes/) is still valid location, let's start using the new root level themes folder, as it seems destined to happily be accepted as the best practice. So create a folder with your theme's name and place it inside DRUPAL_ROOT/themes/

The basic files and structure in your theme is as follows:

- configuration
	- install
		- MYTHEME.settings.yml
- templates
- favicon.ico
- MYTHEME.info.yml
- MYTHEME.libraries.yml
- MYTHEME.theme
- screenshot.png

MYTHEME.settings.yml - [HELP?]
templates directory - a directory in which you can place your custom twig template files for overriding core templates.
favicon.ico default place that Drupal will look? [HELP?]
MYTHEME.info.yml - the basic meta data about your theme (more below)
MYTHEME.libraries.yml - defines css and js libraries and dependencies that can be included in your theme
MYTHEME.theme - custom code for your theme including preprocessing, altering template suggestions and more!
screenshot.png default place that Drupal will look? [HELP?]

Now you are also going to need a place for your custom CSS, javaScript, images, fonts, and other assets. How you organize these in your theme is a bit of personal taste. If you are pulling in these assets from a prototype system such as pattern lab, you may want to have your grunt automation place all of these things into one assets folder organized like so:
assets
  - css
  - js
  - images
  - fonts
  
Or for example if you are developing right in your Drupal theme, with tools such as sass, compass, bundlr, bower, and Grunt you can put your config.rb, Gemfile, Gruntfile.js, etc. right in your theme root.

- configuration
	- install
		- MYTHEME.settings.yml
- css
	- MYTHEME.css
- JS
	- MYTHEME.js
- sass
	- MYTHEME.scss
- templates
- config.rb
- favicon.ico
- Gemfile
- Gemfile.lock
- MYTHEME.info.yml
- MYTHEME.libraries.yml
- MYTHEME.theme
- screenshot.png

However you decide to organize your assets, we will need to let Drupal know where to find things and what to include which I will be covering in a future installment.

### Overview of the info.yml file.

The file called, THEMENAME.info.yml defines the basic meta data about your theme.

Basic .info.yml file
---------------------
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


  name and description - as they will appear on appearance page admin/appearance
  type - "theme" for themes (as opposed to "module" for modules)     
  package - ?? Help Name for grouping things together.
  core - drupal version
  base theme - the parent theme being used. If not using any just omit the line altogether.
  libraries - defining which css and JS libraries will be used
  regions - machine_name: 'Friendly Name' of regions in which you can place blocks.
  stylesheets-override/stylesheets-remove: a list of core stylesheets that you would like to override and a list of that you would like to remove.
  
A note on base themes:
A parent theme's preprocessing code, templates, and css are used by default, however the regions defined in a parent theme are not automatically available to the child them, so you need to define the regions again in your theme.  

## Sidebar quick intro to yml.

Define - templates? a reusable section of html markup which utilizes variables for content and layout logic
