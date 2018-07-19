---
layout: post
title: Category
permalink: /category/
---
<div>
{% for category in site.categories %}
  <div class="">
    {% capture category_name %}{{ category | first }}{% endcapture %}
    <div id="#{{ category_name | slugize }}"></div>
    <h4 class="category-head">{{ category_name }}</h4>
    <ul>
    {% for post in site.categories[category_name] %}
      <li><a href="{{ site.baseurl }}{{ post.url }}">{{post.title}}</a></li>
    {% endfor %}
    </ul>
  </div>
{% endfor %}
</div>

