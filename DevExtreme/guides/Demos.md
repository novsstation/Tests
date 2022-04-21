---
title: Demos
description: 
published: true
date: 2022-04-21T11:08:21.111Z
tags: 
editor: markdown
dateCreated: 2022-04-18T13:12:03.292Z
---

## **Code Rules**

See [Demos Code Rules](https://devexpress.sharepoint.com/:w:/s/devextreme/EYfhf60Q1-xOn4yCH0TFMi4B1uunl-l8z1kUp3N78etmbg?e=oA6g7w)

## **WidgetGallery Staging**

[http://jsserver/Demos-19.1/WidgetsGallery](http://jsserver/Demos-19.1/WidgetsGallery)

[http://jsserver/Demos-19.2/WidgetsGallery](http://jsserver/Demos-19.2/WidgetsGallery)

[http://jsserver/Demos-20.1/WidgetsGallery](http://jsserver/Demos-20.1/WidgetsGallery)

[http://jsserver/Demos-20.2/WidgetsGallery](http://jsserver/Demos-20.2/WidgetsGallery)

[http://jsserver/Demos-21.1/WidgetsGallery](http://jsserver/Demos-21.1/WidgetsGallery)

## **Demo review flow**

Процесс создания новой демки необходимо согласовывать как описано в этой трелло карточке: [https://trello.com/c/s7VDtYQO/155-demo-review-checklist-template](https://trello.com/c/s7VDtYQO/155-demo-review-checklist-template) Больше информации уточняйте у продукт менеджера. 

## **v20.2+ (GitHub) and others (Hg)**

[Alisher Amonulloyev (DevExpress): General демки 20.2 переехали на гитхаб - https:/…](https://teams.microsoft.com/l/message/19:7a8fe7395a2d47288c29cfc421df6cbf@thread.skype/1596530619934?tenantId=e4d60396-9352-4ae8-b84c-e69244584fa4&groupId=8c31b3e5-5870-46b1-92a7-180d13b282ed&parentMessageId=1596530619934&teamName=DevExtreme&channelName=General&createdTime=1596530619934) 

1\. Начиная с версии 20.2 (js, mvc, netcore) демки лежат в [devextreme-demos](https://github.com/DevExpress/devextreme-demos/) репозитории на GitHub .   
 - работаем (подготовка, запуск, добавление) с демками в форке, как описано в [**Readme.md**](https://github.com/DevExpress/devextreme-demos/blob/20_2/README.md). 

**Обращаю внимание**: если есть необходимость в hg репе или форках, то при запуске команд нужно будет ввести полные пути до них (можно скопировать из проводника).  
\- делаем ПР, мержим, через какое-то время синкер подхватит изменения и закоммитит их в hg репу  
\- затягиваем изменения

\- запускаем локально тесты ([инструкция](https://teams.microsoft.com/l/entity/com.microsoft.teamspace.tab.wiki/tab::2bd851b6-bd63-41ab-bde1-8f1c9de4b600?context=%7B%22subEntityId%22%3A%22%7B%5C%22pageId%5C%22%3A12%2C%5C%22origin%5C%22%3A2%7D%22%2C%22channelId%22%3A%2219%3A7a8fe7395a2d47288c29cfc421df6cbf%40thread.skype%22%7D&tenantId=e4d60396-9352-4ae8-b84c-e69244584fa4)) или WG ([инструкция](https://teams.microsoft.com/l/entity/com.microsoft.teamspace.tab.wiki/tab::2bd851b6-bd63-41ab-bde1-8f1c9de4b600?context=%7B%22subEntityId%22%3A%22%7B%5C%22pageId%5C%22%3A93%2C%5C%22origin%5C%22%3A2%7D%22%2C%22channelId%22%3A%2219%3A7a8fe7395a2d47288c29cfc421df6cbf%40thread.skype%22%7D&tenantId=e4d60396-9352-4ae8-b84c-e69244584fa4))

Если необходимо запустить что-то из этого до мержа ПР на гитхабе, то придется вручную скопировать свои изменения в hg репу.

2\. Для других версий демки остаются в hg репе, в папках:  
\- Demos/WidgetsGallery/WidgetsGallery/JSDemos  
\- Demos/WidgetsGallery.MVC/DevExtreme.MVC.Demos  
\- Demos/WidgetsGallery.MVC/DevExtreme.NETCore.Demos  
Вносим изменения, запускаем локально тесты ([инструкция](https://teams.microsoft.com/l/entity/com.microsoft.teamspace.tab.wiki/tab::2bd851b6-bd63-41ab-bde1-8f1c9de4b600?context=%7B%22subEntityId%22%3A%22%7B%5C%22pageId%5C%22%3A12%2C%5C%22origin%5C%22%3A2%7D%22%2C%22channelId%22%3A%2219%3A7a8fe7395a2d47288c29cfc421df6cbf%40thread.skype%22%7D&tenantId=e4d60396-9352-4ae8-b84c-e69244584fa4)) или WG ([инструкция](https://teams.microsoft.com/l/entity/com.microsoft.teamspace.tab.wiki/tab::2bd851b6-bd63-41ab-bde1-8f1c9de4b600?context=%7B%22subEntityId%22%3A%22%7B%5C%22pageId%5C%22%3A93%2C%5C%22origin%5C%22%3A2%7D%22%2C%22channelId%22%3A%2219%3A7a8fe7395a2d47288c29cfc421df6cbf%40thread.skype%22%7D&tenantId=e4d60396-9352-4ae8-b84c-e69244584fa4)) (если необходимо), затем коммитим в hg репу.

**Описание скриптов**:

-   add-demo - скрипт для добавления новой категории, группы и демки в существующее дерево демок. Позволяет добавить новую категорию, группу или демку без ручного модифицирования menuMeta.json, а так же скопировать минимальный набор файлов для демки (заранее подготовленные файлы или с уже существующей демки)
-   launch-demo - скрипт для выбора конкретной демки и запуска ее в http-server. При необходимости, после запуска демки можно открыть второе окно и поменять в пути подход (пример jQuery на Angular) чтобы одновременно тестировать и Angular и jQuery версию демки
-   link-repos - скрипт для создания symlink в репозитории демки на репозиторий DevExtreme (angular, vue, react, etc). Скрипт нужен для написания демок с локальных изменений в продукте. Желателен запуск с администраторскими правами, в случае ошибок рекомендуется запустить "link-repos" еще раз, выбрать unlink и потом снова link.

3\. Некоторые подготовительные скрипты репозитория создают симлинки, поэтому запускать их нужно **под администратором**. И студию для запуска MVC проектов тоже желательно запускать под админом (случаи падения под обычным пользователем бывали). 

## **WidgetsGallery run**

Clone hg repo [https://hg/mobile](https://hg/mobile)

1.  Run as admin: /PrepareWorkspace.cmd. Ensure there are no errors. (This script make \`npm i\` in GitHub folder)
2.  Run as admin: /Packer.cmd. Ensure there are no errors. Ensure that /GitHub/artifacts/npm folder contains `devextreme` and `devextreme-themebuilder` folders.
3.  Run Demos/WidgetsGallery/PrepareDevExtremeBundles.cmd
4.  Run Demos/WidgetsGallery/CloneRwaDemos.cmd
5.  Open /Demos/WidgetsGallery/WidgetsGallery.sln solution is VS, is runned as administrator.
6.  Build and run WidgetsGallery project.
7.  If you want to see NetCore demos, choose DevExtreme.NETCore.Demos project and 'Run new instance'.

## **WidgetsGallery demo code tabs**

By default WG shows all files from demo folder (js approaches) and controller and view (mvc approaches). You should specify files in menuMeta.json to show additional files (AdditionalMvcFiles/BackendFiles). Also files from JSDemos/data folder will be shown (you should use its name somewhere in demo - customers.json e.g.)

## **Use Only Allowed Data Sources in Demos**

> **We should not use not allowed data in demos! All demo data should be approved by PM.**

You can find data for demos from the following sources:

-   Existed demo data (see existed demos)
-   Data from Ray ([Hotel Data](https://teams.microsoft.com/l/entity/com.microsoft.teamspace.tab.wiki/tab::2bd851b6-bd63-41ab-bde1-8f1c9de4b600?context=%7B%22subEntityId%22%3A%22%7B%5C%22pageId%5C%22%3A52%2C%5C%22sectionId%5C%22%3A166%2C%5C%22origin%5C%22%3A2%7D%22%2C%22channelId%22%3A%2219%3A7a8fe7395a2d47288c29cfc421df6cbf%40thread.skype%22%7D&tenantId=e4d60396-9352-4ae8-b84c-e69244584fa4))
-   Allowed third-party data sources (see allowed third-party data sources)

**Allowed Third-Party Data Sources**

-   Wikipedia
-   [https://datahub.io/](https://datahub.io/)
-   [https://www.kaggle.com/](https://www.kaggle.com/)

Datasets from such data sources should have the following licences:

-   [https://opendatacommons.org/licenses/pddl/](https://opendatacommons.org/licenses/pddl/)
-   [https://creativecommons.org/publicdomain/zero/1.0/](https://creativecommons.org/publicdomain/zero/1.0/)

## **PivotGrid demos specificities**

our public cube doesn't support drill-down queries, it's possible to test this using a local server [http://dashboard-sql19/MSOLAP/msmdpump.dll](http://dashboard-sql19/MSOLAP/msmdpump.dll) (see [Teams conversation](https://teams.microsoft.com/l/message/19:b6225178a53c47a4bf3edc5640abf924@thread.skype/1621859165241?tenantId=e4d60396-9352-4ae8-b84c-e69244584fa4&groupId=8c31b3e5-5870-46b1-92a7-180d13b282ed&parentMessageId=1621859165241&teamName=DevExtreme&channelName=Navigation%20Squad&createdTime=1621859165241) and [https://trello.com/c/owmzrV1y/1935-pivotgrid-current-olap-support-state](https://trello.com/c/owmzrV1y/1935-pivotgrid-current-olap-support-state))

## **Widgets Gallery - Internal**

WG has 3 modes

-   Regular - [https://js.devexpress.com/Demos/WidgetsGallery/](https://js.devexpress.com/Demos/WidgetsGallery/)
-   NetCore - [https://demos.devexpress.com/ASPNetCore/](https://demos.devexpress.com/ASPNetCore/)
-   MVC - [https://demos.devexpress.com/ASPNetMvc/](https://demos.devexpress.com/ASPNetMvc/)
-   RWA - in develepment

It is **not** 3 different apps - it is the same app. To allow simple debugging you can set a cookie 'dx-wg-app-mode' to 'mvc', 'netcore', 'rwa', 'regular' in Daily (stage on jsserver) or Debug configuration to switch between modes.

## **Redirects**

When deleting the demo example, you can set up a redirect to some existing example to avoid broken links in tickets and other public resources. You need add record to this file - [https://github.com/DevExpress/devextreme-demos/blob/21\_2/JSDemos/redirects.json](https://github.com/DevExpress/devextreme-demos/blob/21_2/JSDemos/redirects.json), for example, as follows

```plaintext
{​​​​​​​​ "Widget": "Drawer", "Name": "VerticalOpening", "NewWidget": "Drawer", "NewName": "TopOrBottomPosition" }​​​​​​​​,
```

## **Screenshot Testing**

[Over here!](https://teams.microsoft.com/l/entity/com.microsoft.teamspace.tab.wiki/tab::2bd851b6-bd63-41ab-bde1-8f1c9de4b600?context=%7B%22subEntityId%22%3A%22%7B%5C%22pageId%5C%22%3A93%2C%5C%22sectionId%5C%22%3A177%2C%5C%22origin%5C%22%3A2%7D%22%2C%22channelId%22%3A%2219%3A7a8fe7395a2d47288c29cfc421df6cbf%40thread.skype%22%7D&tenantId=e4d60396-9352-4ae8-b84c-e69244584fa4)