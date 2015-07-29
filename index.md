---
layout: archive
permalink: /
title: "Brad Wade"
---

<div class="page-feature">
  <div class="page-image">
    <img src="{{ site.url }}/images/{{ site.image }}" class="page-feature-image" alt="Brad Wade" itemprop="image">
    {% if page.image.credit %}{% include image-credit.html %}{% endif %}
  </div><!-- /.page-image -->
</div><!-- /.page-feature -->

<div class="tiles">
{% for post in site.posts %}
	{% include post-grid.html %}
{% endfor %}
</div><!-- /.tiles -->
