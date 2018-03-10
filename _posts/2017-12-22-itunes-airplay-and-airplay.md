---
id: 100
title: iTunes и внешняя колонка (AirPlay/BlueTooth)
date: 2017-12-22T00:04:19+00:00
author: Alexey S
layout: post
guid: http://42point.com/?p=100
categories:
  - lifehack
tags:
  - airplay
  - alfred
  - apple
  - itunes
  - soft
format: aside
---
Часто при работе дома, транслирую музыку из iTunes на внешнюю колонку [Bowers & Wilkins Z2](https://market.yandex.ru/product/9334841?track=tabs). В свое время я специально искал устройство с поддержкой AirPlay. Самое большое неудобство — невозможность регулировать звук на внешнем устройстве через медиа-клавиши Macbook, <!--more-->так как они отвечают исключительно за системный звук Mac, а значит что бы отрегулировать звук нужно:

  * переключиться в iTunes
  * курсором найти ползунок и изменить звук (либо `⌘↑/↓`)


{% include image.html path="uploads/2017/12/itunes-and-z2.png" path-detail="uploads/2017/12/itunes-and-z2.png" alt="" %}  


Варианта назначить штатными средствами глобальные сочетания клавиш не нашел а поиск по сети подсказал несколько достаточно старых приложений ставить которые желания не было.

## На помощь пришел Alfred.

[Alfred](https://www.alfredapp.com/), как известно, универсальный инструмент для разных задач. Одна из функций которая в очередной раз выручила — workflows.

  1. Создаем новый workflow
  2. Добавляем триггер на основе горячих клавиш (hotkey)<figure>
{% include image.html path="uploads/2017/12/trigger.png" path-detail="uploads/2017/12/trigger.png" alt="" %} 


3. Назначаем интересующее сочетание клавиш.
{% include image.html path="uploads/2017/12/hotkey.png" path-detail="uploads/2017/12/hotkey.png" alt="" %}

4. Добавляем action — iTunes Command и выбираем Volume Up/Down

{% include image.html path="uploads/2017/12/action.png" path-detail="uploads/2017/12/action.png" alt="" %}


Готово!

PS. вот [ссылка](https://s3.eu-central-1.amazonaws.com/com.42/Hotkeys_iTunes.alfredworkflow.zip) на мой файл с Workflow который можно импортировать