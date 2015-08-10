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
assetlist:
  title: Example assets folder
  filelist:
  - name: assets
    tier: 1
    class: fa fa-folder
  - name: css
    tier: 2
    class: fa fa-folder
  - name: js
    tier: 2
    class: fa fa-folder
  - name: images
    tier: 2
    class: fa fa-folder
  - name: fonts
    tier: 2
    class: fa fa-folder
biglist:
  title: Example Drupal 8 Theme Folder Structure
  filelist:
  - name: configuration
    tier: 1
    class: fa fa-folder
  - name: install
    tier: 2
    class: fa fa-folder
  - name: MYTHEME.settings.yml
    tier: 3
    class: fa fa-file-text-o
  - name: css
    tier: 1
    class: fa fa-folder
  - name: MYTHEME.css
    tier: 2
    class: fa fa-file-code-o
  - name: js
    tier: 1
    class: fa fa-folder
  - name: MYTHEME.js
    tier: 2
    class: fa fa-file-code-o
  - name: sass
    tier: 1
    class: fa fa-folder
  - name: MYTHEME.scss
    tier: 2
    class: fa fa-file-code-o
---
configuration
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

## Lessons From the Road

Back in [DATE] I set out on an adventure with Memorial Sloan Kettering and a band of merry Phase2 developers and peeps to begin building the first fully-operational enterprise D8 website. We launched. We were successful. Blah, blah, blah. Over the past year we have learned much. Want to share the real-world secrets we learned to help get everyone comfortable and start adopting Drupal 8.

{% include toc.html %}

## Getting started with a new D8 theme

### Overview of files and folders

When you look into Drupal's root folder, there is a new folder there called "themes" wherein your custom theme folder will reside. While the old D7 path (sites/SITENAME/themes/) is still valid location, let's start using the new root level themes folder, as it seems destined to happily be accepted as the best practice. So create a folder with your theme's name and place it inside DRUPAL_ROOT/themes/

The basic files and structure in your theme is as follows:

<div class="finder-list">
  <div class="finder-list__title">Basic Drupal 8 Theme File Structure</div>
	<div class="finder-list__row odd tier-1"><i class="fa fa-folder"></i> configuration</div>
	<div class="finder-list__row even tier-2"><i class="fa fa-folder"></i> install</div>
	<div class="finder-list__row odd tier-3"><i class="fa fa-file-text-o"></i> MYTHEME.settings.yml</div>
	<div class="finder-list__row even tier-1"><i class="fa fa-folder"></i> templates</div>
	<div class="finder-list__row odd tier-1"><i class="fa fa-file-image-o"></i> favicon.ico</div>
	<div class="finder-list__row even tier-1"><i class="fa fa-file-text-o"></i> MYTHEME.info.yml</div>
	<div class="finder-list__row odd tier-1"><i class="fa fa-file-text-o"></i> MYTHEME.libraries.yml</div>
	<div class="finder-list__row even tier-1"><i class="fa fa-file-code-o"></i> MYTHEME.theme</div>
	<div class="finder-list__row odd tier-1"><i class="fa fa-file-image-o"></i> screenshot.png</div>
</div>

MYTHEME.settings.yml
: [HELP?]

templates directory
: a directory in which you can place your custom twig template files for overriding core templates.

favicon.ico
: default place that Drupal will look? [HELP?]

MYTHEME.info.yml
: the basic meta data about your theme (more below)

MYTHEME.libraries.yml
: defines css and js libraries and dependencies that can be included in your theme

MYTHEME.theme
: custom code for your theme including preprocessing, altering template suggestions and more!

screenshot.png
: default place that Drupal will look? [HELP?]

Now you are also going to need a place for your custom CSS, javaScript, images, fonts, and other assets. How you organize these in your theme is a bit of personal taste. If you are pulling in these assets from a prototype system such as pattern lab, you may want to have your grunt automation place all of these things into one assets folder organized like so:

{% include finder.html finderlist=page.assetlist %}

Or for example if you are developing right in your Drupal theme, with tools such as sass, compass, bundlr, bower, and Grunt you can put your config.rb, Gemfile, Gruntfile.js, etc. right in your theme root.

{% include finder.html finderlist=page.biglist %}

However you decide to organize your assets, we will need to let Drupal know where to find things and what to include which I will be covering in a future installment.

### Overview of the info.yml file.

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
: ?? Help Name for grouping things together.

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

## Sidebar quick intro to yml.

Define - templates? a reusable section of html markup which utilizes variables for content and layout logic
