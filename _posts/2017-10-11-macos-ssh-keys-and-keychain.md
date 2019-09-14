---
title: Хинт про работу с ключами SSH на mac os x
date: 2017-10-11T13:21:22+00:00
author: Alexey S
layout: post
image: uploads/2017/10/Screen-Shot-2017-10-11-at-10.51.12-1-520x300.png
tags:
  - macos
  - manuel
  - ssh
---
Что такое SSH и для чего они нужны лучше чем уже [сказано на Хабре](https://habrahabr.ru/post/122445/) рассказать не смогу. Потому лишь добавлю что внезапно а в версии 10.12.2 macOS обновилась библиотека OpenSSH [^1] и логика работы с ключами. Что конечно же все сломало — ssh-ключи не загружаются после загрузки системы. Что очень неудобно при работе Sourcetree, Github, хостингами да и вообще. Так что подготовил инструкцию больше для себя как исправить включая все шаги.

<!--more-->

1. Создаем ключ если его еще нет. Инструкций с картинками в сети полно, например, на [Github](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).
2. Добавляем его passphrase в системный Keychain `ssh-add -K FULL_PATH_to_PrivateKeyFile`
3. Добавляем его в ssh-agent `ssh-add -A`
4. Добавляем файл config где обязательно указываем следующие параметры:
{% highlight bash %}
Host *
  UseKeychain yes
  AddKeysToAgent yes
{% endhighlight %}
{:start="5"} 
5. Теперь нужно команду `ssh-add -A` автоматически на старте системы. Первый вариант один через скрипт в `~/.bash_profile`:
{% highlight bash %}
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
7. Если не хотим каждый раз вводить пароль — в настройках “связки ключей” снимаем галочку об автоматической блокировке.

{% include image.html path="uploads/2017/10/Screen-Shot-2017-10-11-at-10.51.12-1.png" path-detail="uploads/2017/10/Screen-Shot-2017-10-11-at-10.51.12-1.png" alt="" %}

8. PS для того что бы посмотреть текущие ключи в в агенте `ssh-add -l`


[^1]: [Technical Note TN2449OpenSSH updates in macOS 10.12.2](https://developer.apple.com/library/content/technotes/tn2449/_index.html)
[^2]: [Методы автозагрузки приложений в Mac OS X. LaunchAgents и LaunchDaemons.](http://macdaily.me/howto/startup-applications-in-mac-os-x-launchagents-and-launchdaemons/)

  [Saving SSH keys in macOS Sierra keychain](https://github.com/jirsbek/SSH-keys-in-macOS-Sierra-keychain)