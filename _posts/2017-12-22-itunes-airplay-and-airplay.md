---
id: 100
title: iTunes и внешняя колонка (AirPlay/BlueTooth)
date: 2017-12-22T00:04:19+00:00
author: Alexey S
layout: post
guid: http://42point.com/?p=100
permalink: /itunes-airplay-and-airplay/
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
  * курсором найти ползунок и изменить звук (либо ⌘↑/↓)<figure>

![](http://42point.com/wp-content/uploads/2017/12/itunes-and-z2.png)</figure> 

Варианта назначить штатными средствами глобальные сочетания клавиш не нашел а поиск по сети подсказал несколько достаточно старых приложений ставить которые желания не было.

## На помощь пришел Alfred.

[Alfred](https://www.alfredapp.com/), как известно, универсальный инструмент для разных задач. Одна из функций которая в очередной раз выручила — workflows.

  1. Создаем новый workflow
  2. Добавляем триггер на основе горячих клавиш (hotkey)<figure>

![](http://42point.com/wp-content/uploads/2017/12/trigger.png)</figure> <figure>3. Назначаем интересующее сочетание клавиш.</figure> <figure>![](http://42point.com/wp-content/uploads/2017/12/hotkey.png)</figure> <figure>4. Добавляем action — iTunes Command и выбираем Volume Up/Down</figure> <figure>![](http://42point.com/wp-content/uploads/2017/12/action.png)</figure> 

Готово!

PS. вот [ссылка](https://s3.eu-central-1.amazonaws.com/com.42/Hotkeys_iTunes.alfredworkflow.zip) на мой файл с Workflow который можно импортировать