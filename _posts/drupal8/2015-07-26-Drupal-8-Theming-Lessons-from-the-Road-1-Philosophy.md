---
layout: article
title: Philosophy for early Drupal 8 Theming
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
