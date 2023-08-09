---
layout: single
title: "Книги"
description: "Список книг по теме продуктового менеджмента и его концепций"
date: 2023-06-23
categories:
tags: [tag1, tag2]
toc: true
toc_sticky: true
sidebar:
  nav: "twenty-four"
---

{% for entry in site.data.product-books.list %}

<div>
  <div class="line-header">
    {% assign bookSize = entry.books | size %}
    {% if bookSize == 1 %}
    <h2 id="{{entry.type}}-books">{{ entry.type }}</h2><span class="details">{{ bookSize }} книга</span>
    {% elsif bookSize > 1 %}
    <h2 id="{{entry.type}}-books">{{ entry.type }}</h2><span class="details">{{ bookSize }} books</span>
    {% else %}
    <h2 id="{{entry.type}}-books">{{ entry.type }}</h2><span class="details">I haven't read any books this type. So
      far.</span>
    {% endif %}
  </div>

  <div>
    <!--Book card for each type-->
    <ul class="book-list" style="margin-left: 0; padding-left: 0;">
      {% for book in entry.books %}
      <li style="list-style-type: none;">
        <div class="book-item">
          <a href="{{ book.link }}">
            <img class="cover align-left" src="{{ book.image }}" alt="{{ book.title }}" style="width: 150px;" />
          </a>
          <div class="book-info">
            <h4><a class="book-title" href="{{ book.link }}">{{ book.title }}</a></h4>
            <p class="book-author">{{ book.author }}</p>
            <p>{{ book.description | markdownify }}</p>
            <p class="post-meta">Статус:
              {% if book.completed == 'Читаю' %}
              <span style="color: #EB002B">📖 {{ book.completed }}</span>
              {% elsif book.completed == 'Забросил' %}
              <span style="color: #EB002B">{{ book.completed }} ¯\_(ツ)_/¯ </span>
              {% elsif book.completed == 'Надо перечитать' %}
              <span style="color: #EB002B">📚{{ book.completed }} </span>
              {% else %}
              <span>📗 {{ book.completed | date: "%F" }}</span>
              {% endif %}
              {% if book.audiobook == true %}
              <span> 🎧</span>
              {% endif %}
            </p>
            {% for tag in book.genre %}
            <p> {{ tag }}</p>
            {% endfor %}
          </div>
        </div>
      </li>
      {% endfor %}
    </ul>
  </div>
</div>

{% endfor %}
