---
layout: single
---

Hi there!

My name is Duy Phuong Nguyen (Buzi Nguyen), a PhD candidate at Princeton University working with
Assistant Professor Jaime Fisac.

{% for exp in site.data.experience %}
# {{ exp[0] | capitalize }} Experience

  {% for item in exp[1] %}

  <div class="row">
    <div class="column-logo">
      <img style="float:left;" src="{{ item.logo }}" class="img-logo">
    </div>
    <div class="column-desc">
      <i>{{ item.time }}</i> <br>
      {% if exp[0] == "education" %}
        <b><a href="{{ item.url }}">{{ item.school }}</a></b> - {{ item.location }}<br>
        <i>{{ item.program }}</i><br>
      {% else %}
        <b><a href="{{ item.url }}">{{ item.org }}</a></b> - {{ item.location }}<br>
        <i>{{ item.role }}</i><br>
      {% endif %}
    </div>
  </div>

  {{ item.description }}

  {% endfor %}



{% endfor %}

