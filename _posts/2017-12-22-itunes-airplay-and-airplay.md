---
title: iTunes и внешняя колонка (AirPlay/BlueTooth)
date: 2017-12-22T00:04:19+00:00
layout: single
categories:
  - lifehack
tags:
  - airplay
  - alfred
  - apple
  - itunes
  - soft
---
Часто при работе дома, транслирую музыку из iTunes на внешнюю колонку [Bowers & Wilkins Z2](https://market.yandex.ru/product/9334841?track=tabs). В свое время я специально искал устройство с поддержкой AirPlay. Самое большое неудобство — невозможность регулировать звук на внешнем устройстве через медиа-клавиши Macbook, <!--more-->так как они отвечают исключительно за системный звук Mac, а значит что бы отрегулировать звук нужно:

  * переключиться в iTunes
  * курсором найти ползунок и изменить звук (либо `⌘↑/↓`)


![itunes and z2](/assets/images/uploads/2017/12/itunes-and-z2.png)


Варианта назначить штатными средствами глобальные сочетания клавиш не нашел а поиск по сети подсказал несколько достаточно старых приложений ставить которые желания не было.

## На помощь пришел Alfred.

[Alfred](https://www.alfredapp.com/), как известно, универсальный инструмент для разных задач. Одна из функций которая в очередной раз выручила — workflows.

  1. Создаем новый workflow
  2. Добавляем триггер на основе горячих клавиш (hotkey)<figure>
![trigger](/assets/images/uploads/2017/12/trigger.png)


3. Назначаем интересующее сочетание клавиш.
![hotkey](/assets/images/uploads/2017/12/hotkey.png)

4. Добавляем action — iTunes Command и выбираем Volume Up/Down

![action](/assets/images/uploads/2017/12/action.png)


Готово!

PS. вот [ссылка](https://s3.eu-central-1.amazonaws.com/com.42/Hotkeys_iTunes.alfredworkflow.zip) на мой файл с Workflow который можно импортировать