---
title: Testing
description: 
published: true
date: 2022-04-21T11:14:32.948Z
tags: 
editor: markdown
dateCreated: 2022-04-18T12:45:31.944Z
---

## **Guidelines**

See [Recommendations](https://devexpress.sharepoint.com/:w:/s/devextreme/ESLCAi7OVW5LtMr9C7Fwp9MB_XSSpz88U9zWhokQcrhTng?e=tSETIV)

## **QUnint Tasks**

### **General Info**

QUnit task configs for 20.2 in [DxVCS](https://teams.microsoft.com/l/entity/com.microsoft.teamspace.tab.wiki/tab::2bd851b6-bd63-41ab-bde1-8f1c9de4b600?context=%7B%22subEntityId%22%3A%22%7B%5C%22pageId%5C%22%3A48%2C%5C%22sectionId%5C%22%3A57%2C%5C%22origin%5C%22%3A2%7D%22%2C%22channelId%22%3A%2219%3A7a8fe7395a2d47288c29cfc421df6cbf%40thread.skype%22%7D&tenantId=e4d60396-9352-4ae8-b84c-e69244584fa4): $/CCNetConfig/Server/Config/devextreme-20.2-qunit.xml

Modify a file, "check in" and start the '$configWatcher' task to apply your changes to farm environment (watcher can wait some time until the modified tasks are finished).

For example:

```plaintext
        <cb:scope Constellation="ui.widgets">
          <cb:scope BrowserName="chrome" BrowserDisplayName="Google Chrome"><cb:devextreme_qunit /></cb:scope>
          <cb:scope BrowserName="firefox" BrowserDisplayName="Firefox"><cb:devextreme_qunit /></cb:scope>
          <cb:scope BrowserName="ie" BrowserDisplayName="IE" consoleRunnerTimeout="4200"><cb:devextreme_qunit /></cb:scope>
          <cb:scope BrowserName="edge" BrowserDisplayName="MS Edge" consoleRunnerTimeout="3600"><cb:devextreme_qunit /></cb:scope>
        </cb:scope>
```

### **PivotGrid and store.xmla.tests.js Failures**

Если падают все тесты на [store.xmla.tests.js](https://ciserver/BuildLog/DevExtreme%20QUnit%20tests%20(20.2%20tip,%20jQuery%202,%20Google%20Chrome)/log20210117234158.xml) то с большой долей вероятности отвалился сервак с базой.

Промверить это можно, если попытаться подключиться через SqlServer Management Studio к Analisis Service по урлу

> [http://dashboard-sql19/MSOLAP/msmdpump.dll](http://dashboard-sql19/MSOLAP/msmdpump.dll)

![](/image_2022-04-18_165241383.png)

Если вылетит такая ошибка, то нужно писать ребятам из Dashboard (Дмитрий Зеленов или Олег Лучников в канале

[Denis Kuznetsov (DevExpress): Я ребутнул dashboard-sql19 и тесты поднялись. Что-то с …](https://teams.microsoft.com/l/message/19:ff9da357fdb64c8da0cc517f3395d53f@thread.skype/1610958461506?tenantId=e4d60396-9352-4ae8-b84c-e69244584fa4&groupId=776d973e-cb6f-43e5-940f-c4d33422b8b2&parentMessageId=1610953270310&teamName=Dashboards&channelName=Desktop%20Squad&createdTime=1610958461506)  posted in Dashboards / Desktop Squad at Jan 18, 2021 11:27 AM).

![](/image_2022-04-18_165409201.png)

![](blob:https://teams.microsoft.com/7e3be012-f55c-47a2-9419-3e1bca8b0142)

### **TS Compilation Cases**

Note that these cases never work in run-time.

Guidelines:

-   Each case is wrapped with a function without parameters. This is done for convenience only, the function itself is not the part of the case
-   Function name is the name of the case, so it should explain what is the case about. Use [BDD](https://en.wikipedia.org/wiki/Behavior-driven_development) style, so that <file\_name + function\_name> read as full sentence explaining how it should behave
-   Make function body representing compilation case as small as possible

Example:

```plaintext
// custom_store.ts

export function loadAcceptsPromise() {​​​​​​
  new CustomStore({​​​​​​
    load() {​​​​​​​​​​
      return new Promise(r => r({​​​​​​​​​​}​​​​​​​​​​​​​​​​​ as any))
    }​​​​​​​​​​​​​​​​​
  }​​​​​​​​​​​​​​​​​​​​);
}​​​​​​​​​​​​​​​​​​​​
```