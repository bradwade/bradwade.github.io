---
layout: article
title: Book Outline
image:
  teaser: nature-q-c-800-500-7.jpg
  feature: nature-q-g-1024-256-3.jpg
  credit: Michael Rose #name of the person or site you want to credit
  creditlink: http://mademistakes.com #url to their site or licensing
---

## Philosophy for early D8 theming - managing layout without panels
Most everything is a node.
Place Blocks conditionally.
Switch page level layouts based on node type or other node field.

## Basic folder structure and theme location. Quick list of what each file does. info.yml
Basic .info.yml file
sidebar intro to yml

## Libraries - how to include JS and CSS in your theme

## Twig templates and Classy Basetheme
use classy as base theme and find templates there

## Debug and Turn Cache Off

## Regions and Blocks
Defining Regions
Controlling what blocks go where ** (Tobby, Jonathan help?)
Creating custom blocks
Breadcrumbs
Placing Blocks in Nodes
How to make blocks aware of/contain node content ** (Tobby, Jonathan help?) / Placing node content into blocks.

## THEMENAME.theme

Meta & Link Tags and Favicon
Get path to theme.
Is Front

### preprocess_html
- custom logic to add a body class (or html class?)
- page_attachments_alter
  - add meta tags (to tell IE not to use compatibility mode)
  - add favicons, and related meta tags for icons

### preprocess_page

- get the node variable
- set class and variables for template based on desired layout
- Style drupal_set_message

Follow through to template???

### hook_theme_suggestions_page_alter() ..._node_alter() ..._field_alter ..._views_view_alter()
custom logic to determine which template file to use

### Preprocess Node
various massaging of node variables with custom code.
Place block in node

### other
function mskcc_preprocess_menu_local_task(&$variables) {
  $variables['element']['#link']['url']->setOption('attributes', array('class'=>'mskcc-btn rounded'));
}

function mskcc_preprocess_form(&$variables) {
  $variables['attributes']['class'][] = 'mskcc-form';
  $variables['attributes']['novalidate'] = 'novalidate';
}

### hook_theme() help?
Create variables? available to? 


=================

## 1) Philosophy for early D8 theming - managing layout without panels

## 2) Getting started with a new D8 theme  
Theme location. Folder structure. List of files and quick sentence on each with more detailed explanation of info.yml.
Sidebar quick intro to yml.

## 3) Libraries - how to include JS and CSS in your theme

## 4) Twig templates and Classy Basetheme
Use classy as base theme and find templates there
Some basic twig info.

## 5) Debug mode and Turn Cache Off

## 6) Regions and Blocks
Defining Regions. Controlling what blocks go where. Creating custom blocks. Breadcrumbs. Placing Blocks in Nodes. Placing node content into blocks.

## 7) THEMENAME.theme
preprocessing and suggestions alters. 
How to add custom body/html classes.
How to use custom logic/data to determine which template file to use
Create custom meta & link tags. How to add favicon/icons.
Hot to get path to theme. How to determine is_front.
How to get the node variable when it isn't already defined.
How to style drupal messages. drupal_set_message
hook_theme()
