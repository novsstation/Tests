---
title: Tools
description: 
published: true
date: 2022-04-21T11:14:59.226Z
tags: 
editor: markdown
dateCreated: 2022-04-18T13:01:17.797Z
---

## **DxCorrectorTool**

1.  [https://talk.devexpress.com/t/topic/6237](https://talk.devexpress.com/t/topic/6237) - search 'Corrector'
2.  [https://talk.devexpress.com/t/aka/6762](https://talk.devexpress.com/t/aka/6762)

New version is available [here](https://teams.microsoft.com/l/channel/19%3Ab3023709bb404e64b4fdd034a223ff0c%40thread.skype/tab%3A%3Aecb5daed-2ba1-45f8-8c4f-094cf863c008?groupId=abbb7d3f-3915-466f-a122-ce4e8d81ef30&tenantId=e4d60396-9352-4ae8-b84c-e69244584fa4) (link updated: 11-Aug-21 )

It uses Microsoft authentication, to avoid passing 2FA on each run you can register an account in Windows:

-   Press Win
-   Search for "email and accounts"
-   Press "Add an acoount"
-   ...
-   Profit

Original wiki topic: [here](https://teams.microsoft.com/l/entity/com.microsoft.teamspace.tab.wiki/tab::ecb5daed-2ba1-45f8-8c4f-094cf863c008?context=%7B%22subEntityId%22%3A%22%7B%5C%22pageId%5C%22%3A9%2C%5C%22origin%5C%22%3A2%7D%22%2C%22channelId%22%3A%2219%3Ab3023709bb404e64b4fdd034a223ff0c%40thread.skype%22%7D&tenantId=e4d60396-9352-4ae8-b84c-e69244584fa4)

## **DxVcs**

See this [guide](https://devexpress.sharepoint.com/:w:/s/devextreme/EUNcVOphUr9BrS7Mnn4a-sEBPWB0TegSFrWvK52Pg1c_vQ?e=9DEBl2)

## **Photoshop**

You can connect via RDP to the jsserver (corp\\jsserver). Use buildmaker account

For more details see this [thread](https://teams.microsoft.com/l/message/19:7a8fe7395a2d47288c29cfc421df6cbf@thread.skype/1576593524890?tenantId=e4d60396-9352-4ae8-b84c-e69244584fa4&groupId=8c31b3e5-5870-46b1-92a7-180d13b282ed&parentMessageId=1576593524890&teamName=DevExtreme&channelName=General&createdTime=1576593524890)

## **Tortoise HG & Mercurial**

See the [guide](https://devexpress-my.sharepoint.com/:w:/p/anton_kuznetsov/EY8o79AzuRBFib2NqagSfFIBkQwYWRvy1dyKxNboPQkBdA?e=4VXbIr)

## **TypeScript**

-   [AST Viewer](https://ts-ast-viewer.com/#)
-   [Playground](https://www.typescriptlang.org/play)

## **MSTeams connectors**

Для нотификаций используется Incoming Webhook коннектор. В его натсройках есть URL, который используется для отправки ему сообщений.

Используется коннекстор канала [CI Notifications](https://teams.microsoft.com/l/channel/19%3a3aeb378101f240b9b9c9c71c219e4f68%40thread.skype/CI%2520Notifications?groupId=8c31b3e5-5870-46b1-92a7-180d13b282ed&tenantId=e4d60396-9352-4ae8-b84c-e69244584fa4)

Пользователи этого хука:

-   UnhappyFarmer ($/CCNetConfig/LocalProjects/DevExtreme/neutral/UnhappyFarmer). URL хука используется классом TeamsNotifier.
-   ActiveBugs($/CCNetConfig/LocalProjects/DevExtreme/neutral/ActiveBugs/ActiveBugs). URL хука в Program.cs.
-   [https://github.com/DevExpress/DevExtreme/settings/secrets/actions](https://github.com/DevExpress/DevExtreme/settings/secrets/actions) URL хука в секрете TEAMS\_ALERT

Если нужно вдруг обновить URL, права на хуки у админов команды

## **VS Code**

About disabling telemetry: [https://www.reddit.com/r/privacy/comments/80d8wu/just\_realised\_that\_visual\_studio\_code\_sends/duvaf76/](https://www.reddit.com/r/privacy/comments/80d8wu/just_realised_that_visual_studio_code_sends/duvaf76/)

## **Node.js version manager**

Для простого переключения между версиями ноды Microsoft/Google/npm рекомендует использовать nvm:  
Под винду [https://github.com/coreybutler/nvm-windows](https://github.com/coreybutler/nvm-windows)  
Под линукс [https://tecadmin.net/how-to-install-nvm-on-ubuntu-20-04/](https://tecadmin.net/how-to-install-nvm-on-ubuntu-20-04/)