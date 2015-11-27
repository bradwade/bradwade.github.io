---
layout: archive
permalink: /
title: "About Brad Wade"
image:
  feature: 210And2more-wide.jpg
  credit: Joshua Brandenburg
  creditlink: http://www.drinkandsmile.com/
---

<div class="bio">
  <img src="{{ site.url }}/images/{{ site.data.bio.image }}" alt="Brad Wade" class="bio__image">
  <p class="bio__text" markdown="1">{{ site.data.bio.short }}</p>
  <div class="bio__links">
    {% include icon-list.html iconlist=site.data.bio.links %}
  </div>
</div>

<h2 class="latest-posts-title">Latest Posts</h2>
<div class="tiles">
{% for post in site.posts limit:4%}
	{% include post-grid.html %}
{% endfor %}
</div><!-- /.tiles -->
