---
layout: article
title: 1) Philosophy for early Drupal 8 Theming
subtitle: Lessons from the Road
categories: drupal8
comments: true
share: true
image:
  teaser: triboro-800-500.jpg
  feature: triboro-1140-285.jpg
  credit: Joshua Brandenburg
  creditlink: http://www.drinkandsmile.com/
excerpt: Panels? Display Suite? Context? How can you manage layouts if your tool of choice isn't ready? How can you create a theme without your favorite base theme?
---

## Lessons From the Road

{{ site.data.posts-d8-theming.lessons-excerpt }}

{% include toc.html %}

## Philosophy for early D8 theming

##### (AKA Managing layout without panels...)

In Drupal 7 days, there was much debate on how to manage page and node layout. Which tools would you use? Panels? Display Suite? Context? Perhaps your tool of choice isn't ready for Drupal 8. (None of them were ready when I started.) It might seem daunting to move forward with out your normal set of tools. I'm hoping to cast a vision for how you can move forward. A possible way ahead.

How can we manage various layouts for different pages? The answer: Bare-metal Drupal.

## Embrace core

So the Drupal theming system is predicated on a concept of nested templates. Field templates inside of a node template, inside of a page template, inside of an html template... We need to embrace that and run with it. Despite the... errr... constructive criticism that the Drupal theme layer has received over the years, it actually is a well thought out, powerful, and flexible system. And it has only improved and gotten easier to use in Drupal 8.

Here's how we took advantage of it.

In general, we tried to define as much content as nodes as possible. This made things easier on ourselves by keeping keeping the site more consistent.

The page's particular content (such as the blog's article and pictures) was handled at the node template level. Page templates handled the outer level layout (such as main menus, sidebars, and footers). There were multiple types of node and page layouts. It is possible to handle switching between them based on node type, a node field, or any condition you can write in an if statement. (I'll show you how later in this series.) *Complimentary* content contained in blocks can be conditionally added to regions in each page template. You can conditionally place blocks based on things such as path or node type. With some custom coding you can even create your own set of custom conditions that are available in the UI for all blocks just like the standard core conditions. It's bare-metal drupal and you can do a lot with it.

One problem that is inherent with any nested template system, is the assumptions that get made about which data and content should be made available to which template. When looking at designs it is one of the big questions that Drupal front-end developers/theme layer specialists need to answer: Which elements of this design need to be defined in the node and which in the page. Drupal's initial assumptions are that the node templates get node data, page templates don't. We can place blocks inside regions in page templates, but not inside node template. So how do we handle a sidebar that should have a global menu (page level block), as well as the bio of the author of the node (node level field)? (Panels everywhere was one approach to solve this issue.) I'm not offering one magic bullet solution for Drupal 8 core, but throughout this series I will surface ways of making node data available to the page, showing how to place blocks in nodes, how to get node fields to display in a block, and similar solutions that you may have to employ in the edge-use cases when you have to paint outside of the lines.

## But what about my favorite base theme?

A base theme is an additional theme upon which you can build your custom theme. The parent theme's preprocessing code, templates, and css are used by default. (But the regions defined there are not automatically brought over so you would need to define the regions again in your theme.)

Some developers got in the habit of relying on complex base themes in Drupal 7 life-cycle. At the same time sophisticated tools for creating front-end code have arisen such as sass, grunt, bower, and jslint, which help you create themes quickly from scratch including any js libraries or css frameworks that you may desire. So fear not if your favorite base theme is not available for D8, it's actually an opportunity to give this modern front-end development approach and tools a try.

### What about Classy?
Classy is a core base theme that provides improved markup and css from D7. Classes and styles previously provided in core have been moved out of core and into Classy. It provides the basic classes and styling that you may expect from core D7. Classy should be generally seen and used as the default base theme for Drupal 8 -- similar to using no base theme in Drupal 7. If you know that you want an especially stripped down starting point you can skip using any base theme at all.

Core template files have also been included in Classy. So Classy often proves to be a one-stop place for you to go to look for a core template that you need to override.

Enough of the philosophy and pep talk, in my next post I'll dive into getting started with Drupal 8 themes.
