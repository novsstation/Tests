---
title: Настройка вики
description: 
published: true
date: 2022-04-22T05:57:28.479Z
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

В качестве поискового движка используется Database - PostgreSQL. Настраивается [здесь](/a/search). Используемый словарь лексем - русский.

По умолчанию установлена темная тема и немного подправлены стили (настраивается [здесь](/a/theme)):

```css
.v-main__wrap .layout {
  flex-direction: row-reverse
}

h1 {
  margin-bottom: 30px
}
```

 
Возможность добавления на страницу iframe и время жизни авторизационного [токена](https://github.com/Requarks/blog/blob/master/content/post/security-wiki-js.md) настраивается [здесь](/a/security). На этой же странице отключается авторизация через пару логин/пароль.

## Настройка https и авторизации через Office365

Вначале нужно настроить [https](https://docs.requarks.io/install/ubuntu). На этой же страничке есть возможность обновления https сертификата через Let's Encrypt.

Затем можно настраивать авторизацию через [Azure Active Directory](https://docs.requarks.io/auth/azure)

## Настройка бэкапов

Бэкапы развернуты в github репозитории, согласно этому [гайду](https://docs.requarks.io/storage/git)  
 

> Не забываем, что сама вики находится в контейнере в докере. Поэтому, чтобы достучаться до консоли юзаем:  
>  
> 
> ```plaintext
> sudo docker exec -it wiki bash
> ```