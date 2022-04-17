---
title: Хинт про работу с ключами SSH на mac os x
date: 2017-10-11 13:21:22 00:00
author: Alexey S
layout: single
image: uploads/2017/10/Screen-Shot-2017-10-11-at-10.51.12-1-520x300.png
gallery:
  - url: /assets/images/uploads/2017/10/Screen-Shot-2017-10-11-at-10.51.12-1.png
    image_path: /assets/images/uploads/2017/10/Screen-Shot-2017-10-11-at-10.51.12-1.png
    alt: "placeholder image 1"
    title: "Image 1 title caption"
tags:
  - macos
  - manual
  - ssh
---

Что такое SSH и для чего они нужны лучше чем уже [сказано на Хабре](https://habrahabr.ru/post/122445/) рассказать не смогу. Потому лишь добавлю что внезапно а в версии 10.12.2 macOS обновилась библиотека OpenSSH [^1] и логика работы с ключами. Что конечно же все сломало — ssh-ключи не загружаются после загрузки системы. Что очень неудобно при работе Sourcetree, Github, хостингами да и вообще. Так что подготовил инструкцию больше для себя как исправить включая все шаги.

<!--more-->

1. Создаем ключ если его еще нет. Инструкций с картинками в сети полно, например, на [Github](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).
2. Добавляем его passphrase в системный Keychain 

{% highlight bash %}
$ ssh-add -K /path/to/my/key.pem
{% endhighlight %}

для варианта когда ваша версия macos старше выше чем 12.0 то команда должна выглядеть как:[^5]

{% highlight bash %}
$ ssh-add --apple-use-keychain /path/to/my/key
{% endhighlight %}

Если появляется ошибка `WARNING: UNPROTECTED PRIVATE KEY FILE!`[^4] то необходимо настроить права доступа, дабы другие пользователи в сиcтеме не имели доступ к файлу, а именно запустить команду:
{% highlight bash %}
$ sudo chmod 600 /path/to/my/key
{% endhighlight %} 

ну и поставить такие же права на всю папку `~/.ssh`

{% highlight bash %}
$ sudo chmod 755 ~/.ssh
{% endhighlight %}


{:start="3"}
3. Добавляем ключ в ssh-agent `ssh-add -A`[^3]
4. Добавляем файл или редактируем файл `~/.ssh/config` и вносим параметры параметры:
   {% highlight bash %}
   Host \*
   UseKeychain yes
   AddKeysToAgent yes
   {% endhighlight %}
   {:start="5"}
5. Теперь нужно команду `ssh-add -A` автоматически на старте системы. Первый вариант один через скрипт в `~/.bash_profile`:{% highlight bash %}
   ssh-add -A 2>/dev/null;
{% endhighlight %}
   {:start="6"}
6. другой через файл загрузки в `~/Library/LaunchAgents/` [^2] Содержание файла с расширением .plist:
   {% highlight xml %}
   <?xml version="1.0" encoding="UTF-8"?>
   <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
   <plist version="1.0">
   <dict>
   <key>Label</key>
   <string>ssh-add-a</string>
   <key>ProgramArguments</key>
   <array>
       <string>ssh-add</string>
       <string>-A</string>
   </array>
   <key>RunAtLoad</key>
   <true/>
   </dict>
   </plist>
   {% endhighlight %} 
   {:start="7"}
7. Если не хотим каждый раз вводить пароль — в настройках “связки ключей” снимаем галочку об автоматической блокировке.{% include gallery  %} 

[^1]: [Technical Note TN2449OpenSSH updates in macOS 10.12.2](https://developer.apple.com/library/content/technotes/tn2449/_index.html)
[^2]: [Методы автозагрузки приложений в Mac OS X. LaunchAgents и LaunchDaemons.](http://macdaily.me/howto/startup-applications-in-mac-os-x-launchagents-and-launchdaemons/)
[^3]: для того что бы посмотреть текущие ключи в в агенте `ssh-add -l`.
[^4]:[How to Fix "WARNING: UNPROTECTED PRIVATE KEY FILE!" on Mac and Linux](https://stackabuse.com/how-to-fix-warning-unprotected-private-key-file-on-mac-and-linux/)
[^5]: Обновление от 2022-04-17