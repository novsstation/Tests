---
title: Dependent Products
description: 
published: true
date: 2022-04-21T11:08:56.550Z
tags: 
editor: markdown
dateCreated: 2022-04-18T13:15:11.758Z
---

## **Dashboard wrappers**

В общем и целом картина такая:

-   Для дашборда генерируются врапперы для react, vue, angular
-   Для этого используются наши тулзы и генераторы из репозиториев врапперов
-   Тулзы к ним попадают обычным образом, через npm. Версия сейчас "^3.0.0"
-   Врапперные генераторы попадают к ним тоже через npm (наш локальный Вердацио). Они туда публикуются вместе с остальными пакетами (devexteme, devextreme-react, devextrem-react-generator, etc.). Пакет с генератором публикуется, если таска найдет в его package.json версию, которая новее той, которая уже опубликована на Вердацио
-   Посмотреть, какие у дашбордов используются версии тулзов и генераторов можно тут:
    -   [https://github.com/DevExpress/dashboards/blob/21\_2/src/dashboard-react-generator/package.json](https://github.com/DevExpress/dashboards/blob/21_2/src/dashboard-react-generator/package.json)
    -   [https://github.com/DevExpress/dashboards/blob/21\_2/src/dashboard-vue-generator/package.json](https://github.com/DevExpress/dashboards/blob/21_2/src/dashboard-vue-generator/package.json)
    -   [https://github.com/DevExpress/dashboards/blob/21\_2/src/dashboard-angular-generator/package.json](https://github.com/DevExpress/dashboards/blob/21_2/src/dashboard-angular-generator/package.json)