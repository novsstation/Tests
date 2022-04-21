---
title: Настройка вики
description: 
published: true
date: 2022-04-21T11:15:43.890Z
tags: 
editor: markdown
dateCreated: 2022-04-19T11:07:18.574Z
---

## Установка

Follow this [guide](https://docs.requarks.io/install/ubuntu)

Сама виртуалка находится по адресу: 20.224.248.58  
Логин и пароль от виртуалки есть у Ильи Харченко, Сергея Звягина, Жени Жаворонкова и Сергея Авраменко.  
Достучаться до консоли можно например, через [putty](https://www.putty.org) (или любой другой привычный вам ssh клиент).  
  
Возможность добавления на страницу iframe и время жизни авторизационного [токена](https://github.com/Requarks/blog/blob/master/content/post/security-wiki-js.md) настраивается [здесь](/a/security).   
На этой же странице отключается авторизация через пару логин/пароль.

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