---
title: Docke for qunit
description: 
published: true
date: 2022-04-18T13:22:26.685Z
tags: 
editor: markdown
dateCreated: 2022-04-18T11:25:14.372Z
---

## Ставим Docker for Windows (https://docs.docker.com.docker-for-windows/install/)

> Для повышения скорости Проверяем наличие WSL2:

## Скачиваем образ
Нужно сделать только один раз для определенной версии:
> **docker pull devexpress/devextreme-build:21_1**

Это стандартный devextreme образ именно он используется для прогона QUnit тестов в drone на github. Версии не сильно важны т.е. можно условно использую образ от 21_1 прогонять тесты для 20_2 или 21_2, но могут быть накладки.

## Запуск
На локальной машине завпускаем и дожидаемся готовности QUnit сервака:
> **npm run dev**

Именно к нему и будет коннектиться Chrome браузер запущенный в докере (ключик -e LOCAL=true). 

Браузер в докере может быть запущен в headless или обычном режиме.
Ниже приведены команды для запуска в одном из эитм режимов. Перед выполнением команд необходимо заменить:
* ***{constel}***: export, misc, ui, ui.widgets, ui.editors, ui.grid, ui.scheduler, viz, renovation
* ***{version}*** версия предварительно стянутого образа

**${PWD}** указывает на текущий каталог поэтому запускать надо из рута каталога Devextreme

### *Для запуска тестов в headless chrome:*
> **docker run --rm -ti -e TARGET=test -e JQUERY=true -e CONSTEL={constel} -e BROWSER=chrome -e LOCAL=true -p 9222:9222 -v ${PWD}:/devextreme devexpress/devextreme-build:{version} ./docker-ci.sh**

Затем открываем локальный браузер и коннектимся к headless браузеру (должен быть запущен на 9222 порту): 
> **chrome://inspect**


### *Для запуска тестов в chrome:*
> **docker run --rm -ti -e TARGET=test -e JQUERY=true -e CONSTEL=*{constel}* -e NO_HEADLESS=true -e BROWSER=chrome -e LOCAL=true -p 5900:5900 -v ${PWD}:/devextreme devexpress/devextreme-build:*{version}* ./docker-ci.sh**

Затем запускаем VNC (https://www.realvnc.com/en/connect/download/viewer/windows/) и коннектимся **localhost:5900**

### *Замечания*

Работа с VNC более удобна так, как у там открывается полноценный браузер, зато headless более быстрый.

После того как вы запустите докер образ в консоли будет выводится сообщение о прохождении тестов. Коннектиться к браузеру в образе не объязательно это необходимо только если вы хотите детально разобраться в проблемах.

Если вы часто запускаете определенный constel то целесообразно сделать скрипт для запуска



