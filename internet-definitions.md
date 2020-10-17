---
title: Интернет термины
date: 2020-06-05T22:27:53+00:00
layout: single
---
Часто бывает необходимо подобрать правильно определение для договора или элементарного соглашения, а иногда найти простые слова чтобы объяснить клиенту/партнеру о чем идет речь…
* * *


{% assign defi = site.data.definitions.list | sort: "definition" %}

<dl>
  {% for def in defi %}
  <dt id="{{ def.definition }}"> {{ def.definition | markdownify }}</dt>
  <dd>
  {{ def.description | markdownify }}
  {{ def.descriptionAlt | markdownify }} 
  <!-- <ol>
    {% for li in def.li %}
      <li>
        {{ li }};
      </li>
      
    {% endfor %}
  </ol> -->
</dd>
  {% endfor %}
</dl>