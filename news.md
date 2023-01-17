---
layout: single
title: News
permalink: /news/
---

{% assign items = site.data.news | sort: 'date' | reverse %}
{% for item in items %}
<div>
  <span class="news-date">{{ item.date }}</span>
  {% for label in item.label %}
    <span class="news-label {{ label }}">{{ label }}</span>
  {% endfor %}
</div>
<div markdown="1" class="news-item">
  <h3><a href="{{ item.url }}">{{ item.title }}</a></h3>
  ![]({{ item.img }}){: .news-photo}
  {{ item.description }}
</div>
{% endfor %}