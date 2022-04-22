---
title: Настройка вики
description: 
published: true
date: 2022-04-22T06:20:18.331Z
tags: 
editor: markdown
dateCreated: 2022-04-19T11:07:18.574Z
---

## Установка

Follow this [guide](https://docs.requarks.io/install/ubuntu)

У нас развернуто 2 инстанса вики:
- производственная (https://wiki.devexpress.devx [20.224.248.58])
- социальная (... [52.232.13.106])

Соответственно, публичный IP для виртуалок находится по адресам: 20.224.248.58 и 52.232.13.106. Логин и пароль от виртуалок есть у Ильи Харченко, Сергея Звягина, Жени Жаворонкова и Сергея Авраменко.  

Достучаться до консоли можно например, через [putty](https://www.putty.org) (или любой другой привычный вам ssh клиент).

## Настройки

В качестве поискового движка используется Database - PostgreSQL. Настраивается [здесь](/a/search).
Используемый словарь лексем - русский.

По умолчанию установлена темная тема и немного подправлены стили (настраивается [здесь](/a/theme)):

```css
.v-main__wrap .layout {
  flex-direction: row-reverse
}

h1 {
  margin-bottom: 30px
}

header .breadcrumbs-nav {
  pointer-events: none;
}
```

 
Возможность добавления на страницу iframe и время жизни авторизационного [токена](https://github.com/Requarks/blog/blob/master/content/post/security-wiki-js.md) настраивается [здесь](/a/security). На этой же странице отключается авторизация через пару логин/пароль.

## Настройка https и авторизации через Office365

Был придуман очень гибкий механизм чтобы не париться с продлением и актуализацией сертификатов. Есть настроенный балансировщик, который проксирует запросы к домену на публичный айпишник с нужными портами. Поэтому сертификат настраивать не нужно и файлик конфига, который в контейнере расположен по пути root/wiki/config.yml имеет все дефолтные настройки из этого [гайда](https://docs.requarks.io/install/ubuntu):

```yml
port: 3000
bindIP: 0.0.0.0
db:
  type: $(DB_TYPE)
  host: '$(DB_HOST)'
  port: $(DB_PORT)
  user: '$(DB_USER)'
  pass: '$(DB_PASS)'
  db: $(DB_NAME)
  storage: $(DB_FILEPATH)
  ssl: $(DB_SSL)
ssl:
  enabled: $(SSL_ACTIVE)
  port: 3443
  provider: letsencrypt
  domain: $(LETSENCRYPT_DOMAIN)
  subscriberEmail: $(LETSENCRYPT_EMAIL)
logLevel: $(LOG_LEVEL:info)
logFormat: $(LOG_FORMAT:default)
ha: $(HA_ACTIVE)

```

Затем можно настраивать авторизацию через [Azure Active Directory](https://docs.requarks.io/auth/azure)

## Настройка бэкапов

Бэкапы развернуты в github репозитории, согласно этому [гайду](https://docs.requarks.io/storage/git)  
 

> Не забываем, что сама вики находится в контейнере в докере. Поэтому, чтобы достучаться до консоли юзаем:  
> 
> ```plaintext
> sudo docker exec -it wiki bash
> ```

