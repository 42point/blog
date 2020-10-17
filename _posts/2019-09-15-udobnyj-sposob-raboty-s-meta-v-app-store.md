---
layout: single
title: "Как работать с мета-данными в appstore connect"
description: "Немного магии на каждый день"
date: 2019-09-14T22:52:54+03:00
categories:
tags: [apple, appstore]
---

В отличии от Google Play Console, Appstore Connect крайне недружелюбен к менеджеру которому нужно подготовить материалы на нескольких языках для публикации новых версий приложения.

<!--more-->

Поэтому спасением при большом количестве приложение и частых релизах может выступить [Fastlane Deliver](https://docs.fastlane.tools/actions/deliver/). Инструмент позволит автоматизировать:

1. Загрузку, буквально, сотен скриншотов для разных языков и платформ.
2. Обновление тесктовой мета-информации для каждого из языков отдельно: keywords, description, release_notes, name etc.
3. Обновление данных in-app покупок
4. Переиспользование текущих данных

## Как работать с этим?

К сожалению какое-то понимание работы с командной строкой быть должно, хотя бы до уровня “_запустить вот эти вот команды_”.

## Setup

1. Установить xcode. Да, это неизбежное зло.
2. Установить fastlane: `brew cask install fastlane`
3. Перейти в папку проекта

```
mkdir PROJECT-meta
cd PROJECT-meta
```

4. Инициализируем проект fastlane: `fastlane init`
5. Скачиваем существующие метаданные: `Fastlane deliver `. В процессе естественно нужно будет указать креденшиалс и Bundle ID вашего приложения.
   Команда успешно скачивает все данные и создает структуру папок под языки и скриншоты ![](/assets/images/uploads/2019/finder.png)
6. Вносим изменения, если нужно
7. Создаем новую версию в Appstore (можно просто поменять значение `app_version` в Deliverfile).
8. Запускаем`fastlane deliver`. Команда уточнит от чьего имени и что именно вы загружаете а также предложит просмотреть превью всей мета информации.
9. Подтверждайте превью, немного ожидания и PROFIT!

В командной строке получите приятный отчет:

```
[20:54:07]: ✅  Passed: No negative  sentiment
[20:54:07]: ✅  Passed: No placeholder text
[20:54:07]: ✅  Passed: No mentioning  competitors
[20:54:07]: ✅  Passed: No future functionality promises
[20:54:07]: ✅  Passed: No words indicating test content
[20:54:07]: ✅  Passed: No curse words
[20:54:07]: ✅  Passed: No words indicating your IAP is free
[20:54:07]: 😵  Failed: Incorrect, or missing copyright date→ using a copyright date that is any different from this current year, or missing a date
[20:54:31]: ✅  Passed: No broken urls
```

В нашем случае при локализации на 8 языков экономия составит до 2 часов времени.

## Дополнительно

Рекомендую также настроить:

### Appfile:

```
app_identifier("you app bundle id") # The bundle identifier of your app
apple_id("your apple id") # Your Apple email address
```

### Deliverfile

```
app_version "2.6.8"
submit_for_review true
force true # Set to true to skip PDF verification
phased_release true
skip_screenshots false
use_live_version false # use current meta
automatic_release false

precheck_include_in_app_purchases false # если не используете inapp
```
