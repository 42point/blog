---
layout: post
title: "Как временно отключить заставку и сон вашего Macbook"
description: "Управляем питанием и отключением дисплея macOS через terminal"
date: 2018-02-18T08:39:18+03:00
author: Alexey S
categories:
  - 
tags: [macos, terminal]
---

Представим, у вас важная презентация и нужно запретить mac’у отключать дисплей, или вы смотрите новую серию Игры престолов и не хочется все время дергать курсор, дабы дисплей не погас.  Или выполняется важный расчет который остановиться если Macbook  заснет. Может помочь маленькое бесплатное приложение [Caffeine](http://lightheadsw.com/caffeine/) или можно воспользоваться стандартной командой `caffeinate` в терминале, которая делает тоже самое но предоставляет больше гибкости.

<!--more-->

Как у любой терминальной команды, у `caffeinate` свои ключи:

```bash
-t # таймер в секундах
-d # не отключать дисплей
-i # не уводить в ситему в сон 
-m # запрет уводить диски в сон
-s # запрет машине уходить в сон когда 
-u # имитирует дейтсвия текущего пользователя
```
Как можно использовать?

#### Запретить уходить в сон в течении часа

`caffeinate -t 3600 &`

Амперсанд `&` позволит выполнить команду в фоне и освободить командную строку для дальнейшего использования.
Параметр `-t 3600`  задает таймаут в 3600 секунд что равно 1-му часу.

#### Не отключать дисплей и не запускать заставку 

`caffeinate -d`

#### Не засыпать пока выполняется скрипт или процесс

`caffeinate -i long_running_script.sh`


[Take Control of Your Mac's Sleep Functions with These Commands « Mac Tips :: Gadget Hacks](https://mac-how-to.gadgethacks.com/how-to/take-control-your-macs-sleep-functions-with-these-commands-0168109/)
[All about Energy Saver idle and sleep modes in Mac OSX](http://blog.macoptimizerpro.com/2016/05/24/all-about-energy-saver-idle-and-sleep-modes-in-mac-osx/)

