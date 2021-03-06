[![Build Status](https://travis-ci.org/erjanmx/salam-bot.svg?branch=master)](https://travis-ci.org/erjanmx/salam-bot)

# Салам бот

Бот для мессенджера [NambaOne](https://namba1.co/) победивший в конкурсе 'BattleBot' устроенной создателями мессенджера

Позволяет связать двоих случайных пользователей в один чат позволяя им общаться между собой не раскрывая свои настоящие личности

#### Демонстрация
![Imgur](http://i.imgur.com/rNPY46j.gif)

## Установка

Необходим `python3`, `pip` и `virtualenv`

```
virtualenv venv
source venv/bin/activate
pip install -r requirements.txt

cp .env.example .env
```

После, необходимо задать настройки приложения и подключения к базе в `.env` (или задать значения в переменных окружения)

и выполнить создание необходимых таблиц используя команду для миграции

```
orator migrate -c config/settings.py -p database/migrations/ -f
```

### Закрытие неактивных чатов

Если после создания чата собеседник не ответил в течение трех минут то чат должен быть закрыт с уведомлением обоих сторон

Для этого необходимо поставить вызов по расписанию endpoint-a приложения с соответствующими параметрами, а именно

```
curl -X POST \
  'url' \
  -H 'content-type: application/json' \
  -d '{"event":"cron/close_idle_chats","data":""}'
```
