---
layout: archive
permalink: /
title: "About Brad"
image:
  teaser: nature-q-c-800-500-7.jpg
  feature: StoneBarnsWideShort-B-L1038449.jpg
  credit: Steve Wu #name of the person or site you want to credit
  creditlink: http://www.stevenwuphoto.com/ #url to their site or licensing
---

<div class="bio">
<img src="{{ site.url }}/images/bradwade-crop-6U9O0340.jpg" alt="Brad Wade" class="bio__image">
<p class="bio__text">I am a front end web developer, drupal specialist, and a musician. Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor. Aenean massa.</p>
<ul class="bio__links">
  <li><a>linkedin</a></li>
  <li><a>resume</a></li>
  <li><a>twitter</a></li>
  <li><a>drupal.org</a></li>
  <li><a>github</a></li>
</ul>
</div>

<h2 class="latest-posts-title">Latest Posts</h2>
<div class="tiles">
{% for post in site.posts limit:4%}
	{% include post-grid.html %}
{% endfor %}
</div><!-- /.tiles -->
