---
layout: article
title: Philosophy for early Drupal 8 Theming
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

## Philosophy for early D8 theming 
(Managing layout without panels...)

Getting started with a D8 theme site?
In D7 days debate on how manage layout. Which tools would you use? Panels? Display Suite? Context? It might seem daunting to move forward with out your normal set of tools. I'm hoping to cast a vision for how you can move forward. A possible way ahead. 


Well, currently, for better or worse, in D8 you don't have to decide on which contrib tools to use, because none of them are ready yet. So what are we left with? How can we manage various layouts for different pages? Bare-metal Drupal.

### Embrace the node.

So the Drupal theming system is predicated on a concept of nested templates. Field templates inside of a node template, inside of a page template, inside of an html template...
We need to embrace that and run with it. Despite the... errr... constructive criticism that the Drupal theme layer has received over the years, it actually is a well thought out, powerful, and flexible system. And it has only improved and gotten easier to use in Drupal 8. 
Here's how we took advantage of it 

In general, we tried to define as much content as nodes as possible. This made things easier on ourselves by keeping keeping the site more consistent.

The page's particular content (such as the blog's article and pictures) was handled at the node template level. Page templates handled the outer level layout (such as main menus, sidebars, and footers). There were multiple types of node and page layouts. It is possible to handle switching between them based on node type, a node field, or any condition you can write in an if statement. *Complimentary* content contained in blocks can be conditionally added to regions in each page template. Standard conditions [get list from Drupal] or even create custom conditions. It's bare-metal drupal and you can do a lot with it.

One problem that is inherent with any nested template system, is the assumptions that get made about which data and content should be made available to which template. When looking at designs it is one of the big questions that Drupal front-end developers/theme layer specialists need to answer: Which elements of this design need to be defined in the node and which in the page. Drupal's initial assumptions are that the node templates get node data, page templates don't. We can place blocks inside regions in page templates, but not inside node template. So how do we handle a sidebar that should have a global menu (page level block), as well as the bio of the author of the node (node level field)? (Panels everywhere was one approach to solve this issue.) I'm not offering one magic bullet solution for Drupal 8 core, but throughout this series I will surface ways of making node data available to the page, showing how to place blocks in nodes, how to get node fields to display in a block, and similar solutions that you may have to employ in the edge-use cases when you have to paint outside of the lines.

### But what about my favorite base theme?

A base theme is an additional theme upon which you can build your custom theme. The parent theme's preprocessing code, templates, and css are used by default. (But the regions defined there are not automatically brought over so you would need to define the regions again in your theme.)  


Some developers got in the habit of relying on complex base themes in Drupal 7 life-cycle. At the same time sophisticated tools for creating front-end code have arisen such as sass, grunt, bower, jslint, which help you create themes quickly from scratch including any js libraries or css frameworks that you may desire. So fear not if your favorite base theme is not available for D8, give this new approach a try. For more information about my/Phase2 approach to front end development (for Drupal and other projects) checkout this other blog by Jake Love/Evan Lovely.

#### What about Classy?
Classy is a core base theme that provides improved markup and css from D7. Classes and styles previously provided in core have been moved out and into Classy. It provides the basic classes and styling that you may expect from core D7. Classy should be generally seen and used as the default base theme for Drupal 8. Similar to using no base theme in Drupal 7. If you know that you want an especially stripped down starting point you can skip using any base theme at all.

Core template files have also been included in classy. So Classy often proves to be a one-stop place for you to go to look for a core template that you need to override.

Enough of the philosophy and pep talk, let's get started with some how-to...

## 2) Getting started with a new D8 theme  

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
