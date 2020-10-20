---
layout: single
title: "Уведомления Jenkins в Telegram"
description: ""
date: 2020-10-19T22:00:00+03:00
categories:
tags: [Jenkins, manual]
---


Одно из правил работы с CI — все должны видеть статус сборок, тоесть синхронизация. А что может быть лучше чем уведомление о неудачном, или напротив удачном, билде в чате.

1. [3cky/jenkins-telegram-uploader-plugin: Jenkins CI post-build action that uploads artifacts generated during build process to Telegram chats.](https://github.com/3cky/jenkins-telegram-uploader-plugin)
2. [jenkinsci/telegram-notifications-plugin: This plugin allows you to send messages from Jenkins jobs to Telegram chat.](https://github.com/jenkinsci/telegram-notifications-plugin)
3. Использовать секцию пост-функций в пайплайне.


Третий вариант более универсален, ну и с первым плагином я потратил очень много времени но таки и не смог его запустить.


## Настраиваем бот
### Создаем новый бот и канал для уведомлоений.
Находим @botfather и следуя инструкции создаем нового бота. Важно получить токен бота. Токен позволит любому управлять вашим ботом.

![bot father](/assets/images/uploads/2020/10/botfather.png)

Создаем новый канал и добавляем в него ново-созданного бота с правами админа, нужно для публикации новых сообщений.

### Получаем iD чата для отправки уведомлений
Через адресную строку браузера делаем запрос 
```
https://api.telegram.org/bot<TOKEN>/getUpdates
```
Где меняем `<TOKEN>` на значение из пункта создания бота.

Ответ на запрос:
```json
{
    "ok": true,
    "result": [
        {
            "update_id": 151985646,
            "channel_post": {
                "message_id": 3,
                "chat": {
                    "id": -1001459789606,
                    "title": "Leroy",
                    "type": "channel"
                },
                "date": 1603123407,
                "text": "/sub",
                "entities": [
                    {
                        "offset": 0,
                        "length": 4,
                        "type": "bot_command"
                    }
                ]
            }
        },
    ]
}
```

Нужно сохранить chat.id и сохранить знак `-` перед числом, это полный идентификатор.

## Готовим Jenkins
### Настраиваем переменные для авторизации API
Прежде всего добавляем в раздел credentials jenkins id чата, в который будем отсылать сообщения и token созданного бота.
1. Manage Jenkins -> Manage Credentials
![](/assets/images/uploads/2020/10/domain.png)
2. Для уведомлений в телеграмм создаем новый домен.
![](/assets/images/uploads/2020/10/cred.png)
3. Добавляем переменную для ID чата и отдельно переменную для токена созданного бота. Указываем пронятные ID для дальнейшей подстановки переменных.
![](/assets/images/uploads/2020/10/chatId.png)
### Настриваем пайплайн
Предположим уже настроен pipeline через Jenkinsfile. Осталось добавить к нему [post-секцию](https://www.jenkins.io/doc/book/pipeline/syntax/#post)

```groovy
pipeline {
    agent any
    stages {
        
        stage('Checkout') {
            steps {
                echo 'Checkout..'
                checkout scm
            }
        }
        stage('Build') {
            steps {
            // script here
            }
            echo 'Done'
            }
        }
        stage('Publish') {
            steps {
			    // script here
                echo "Deployed Successfully!"
            }
        }
    }
        post {
            success {            
            // script here
			}
            aborted {             
            // script here
			}
            failure {
            // script here
            }
       }
}    

```

Post-секция выполняется независимо от результата стадий основного пайплайна. И именно в нем будут действия для отправки уведомлений.

Все указанные условия должны содержат выполняемые скрипты:

```groovy
 post {
     success { 
        withCredentials([string(credentialsId: 'botSecret', variable: 'TOKEN'), string(credentialsId: 'chatId', variable: 'CHAT_ID')]) {
        sh  ("""
            curl -s -X POST https://api.telegram.org/bot${TOKEN}/sendMessage -d chat_id=${CHAT_ID} -d parse_mode=markdown -d text='*${env.JOB_NAME}* : POC *Branch*: ${env.BRANCH_NAME} *Build* : OK *Published* = YES'
        """)
        }
     }

     aborted {
        withCredentials([string(credentialsId: 'botSecret', variable: 'TOKEN'), string(credentialsId: 'chatId', variable: 'CHAT_ID')]) {
        sh  ("""
            curl -s -X POST https://api.telegram.org/bot${TOKEN}/sendMessage -d chat_id=${CHAT_ID} -d parse_mode=markdown -d text='*${env.JOB_NAME}* : POC *Branch*: ${env.BRANCH_NAME} *Build* : `Aborted` *Published* = `Aborted`'
        """)
        }
     
     }
     failure {
        withCredentials([string(credentialsId: 'botSecret', variable: 'TOKEN'), string(credentialsId: 'chatId', variable: 'CHAT_ID')]) {
        sh  ("""
            curl -s -X POST https://api.telegram.org/bot${TOKEN}/sendMessage -d chat_id=${CHAT_ID} -d parse_mode=markdown -d text='*${env.JOB_NAME}* : POC  *Branch*: ${env.BRANCH_NAME} *Build* : `not OK` *Published* = `no`'
        """)
        }
     }

 }

```

Где: 
- строка начинающаяся с `withCredentials` декларирует переменные для подмены в запросе.
- текст отправляется в формате `markdown`.

Запускаем билд и при успехе получаем уведомление:
![result](/assets/images/uploads/2020/10/result.jpeg)