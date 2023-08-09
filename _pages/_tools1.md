---
title: Инструменты
date: 2020-09-12T23:43:21+00:00
layout: single
permalink: /tools/
---

Иногда меня спрашивают какой софт использую для тех или иных задач. У меня есть
странная тяга к нативным приложениям, и в моем списке наверняка будут те что
можно заменить онлайновыми инструментами. Возможно что-то покажется вам
интересным и полезным. {% for item in site.data.tools.list %}

<!-- start type-->

<div class="{% if site.scrollappear_enabled %}scrollappear{% endif %}">
  <h2>{{ item.type }}</h2>

{% for tool in item.tool %}

  <h4 id="{{ tool.title | slugify }}">
    <a href="{{ tool.link }}" target="_blank">{{ tool.title }}</a>
    <a href="{{ tools | relative_url }}#{{ tool.title | slugify }}">#</a>
  </h4>
  <p>{{ tool.desc | markdownify }}</p>
  {% endfor %}
</div>
<!-- end header -->
{% endfor %}
