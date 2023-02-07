---
title: Инструменты
date: 2020-09-12T23:43:21+00:00
layout: single
permalink: /tools/
---

Иногда меня спрашивают какой софт использую для тех или иных задач. У меня есть
странная тяга к нативным приложениям, и в моем списке наверняка будут те что
можно заменить онлайновыми инструментами. Возможно что-то покажется вам
интересным и полезным.

{% for item in site.data.tools.list %}

<!-- start type-->

<!-- <table>
<colgroup>
<col width="30%" />
<col width="70%" />
</colgroup>
<thead>
<tr class="header">
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td markdown="span">First column **fields**</td>
<td markdown="span">Some descriptive text. This is a markdown link to [Google](http://google.com). Or see [some link][mydoc_tags].</td>
</tr>
<tr>
<td markdown="span">Second column **fields**</td>
<td markdown="span">Some more descriptive text.
</td>
</tr>
</tbody>
</table>

 <h3>{{ item.type }}</h3> -->

{% for tool in item.tool %}

  <h4 id="{{ tool.title | slugify }}">
    <a href="{{ tool.link }}">{{ tool.title }}</a>
    <a href="{{ tools | relative_url }}#{{ tool.title | slugify }}">#</a>
  </h4>
  <p>{{ tool.desc | markdownify }}</p>
  {% endfor %}
</div>
<!-- end header -->
{% endfor %}
