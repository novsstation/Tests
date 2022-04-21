---
title: CCTray & Farm
description: 
published: true
date: 2022-04-21T11:07:13.469Z
tags: 
editor: markdown
dateCreated: 2022-04-18T12:42:51.738Z
---

## **Волонтерство на ферме**

See this thread: [Волонтерство на ферме](https://teams.microsoft.com/l/message/19:7a8fe7395a2d47288c29cfc421df6cbf@thread.skype/1559573858499?tenantId=e4d60396-9352-4ae8-b84c-e69244584fa4&groupId=8c31b3e5-5870-46b1-92a7-180d13b282ed&parentMessageId=1559573858499&teamName=DevExtreme&channelName=General&createdTime=1559573858499) 

## **GitHub commits notifications**

Нужно указать в CCTray имя (точнее, два имени), которое указывается в поле author коммитов, сделанных через сам GitHub (мерж PR - это коммит, сделанный через GitHub). Теоретически, GitHub должен использовать username (логин), но на практике - используется name (публичное имя профиля). Поэтому в CCTray нужно указать **_оба имени через точку с запятой_**:

![](blob:https://teams.microsoft.com/5ae1cfe2-18e4-47a0-aead-31989328d67f)

For more details see this [thread](https://teams.microsoft.com/l/message/19:7a8fe7395a2d47288c29cfc421df6cbf@thread.skype/1554905786133?tenantId=e4d60396-9352-4ae8-b84c-e69244584fa4&groupId=8c31b3e5-5870-46b1-92a7-180d13b282ed&parentMessageId=1554905786133&teamName=DevExtreme&channelName=General&createdTime=1554905786133). And [this one](https://teams.microsoft.com/l/message/19:1f90738df26145b4b7aadcfcadc0cd87@thread.skype/1559647338499?tenantId=e4d60396-9352-4ae8-b84c-e69244584fa4&groupId=8c31b3e5-5870-46b1-92a7-180d13b282ed&parentMessageId=1559647338499&teamName=DevExtreme&channelName=Grids&createdTime=1559647338499).

![](/image_2022-04-18_165007918.png)

## **Adding a WG Task**

**dxVCS**

1\. Открой файл **$/CCNetConfig/Server/Config/devextreme-18.2-testcafe.xml**

2\. Найди группу **<!-- WidgetsGallery -->**

3\. Там разложены таски по подходам с конфигами вида

<cb:scope SectionNumber="12" *SectionName="Scheduler"><cb:devextreme\_testcafe\_demos\_widgetsgallery/></cb:scope>*

4. **SectionNumber** \- порядковый номер, **SectionName** \- название раздела в WidgetsGallery, у которого вырезаны пробелы и дефисы.

5\. После добавления нужных изменений не забудь зачекинить файл.

**dxCCTray**

6\. Запусти таску **$configWatcher**

7\. После того, как она прогонится, появятся новые таски, сконфигурированные тобой в dxVCS. Запусти их.

**ScreenshotReporter**

8\. Нужно подготовить PR в [testcafe-visual-testing](https://github.com/DevExpress/testcafe-visual-testing). Можно ориентироваться на предыдущие [PR](https://github.com/DevExpress/testcafe-visual-testing/pull/26/files)

## **DXCCNet Manual**

[http://ccnet.devexpress.devx/ccnet/doc/](http://ccnet.devexpress.devx/ccnet/doc/)

## **RDP connection**

You can connect to the worker carrying your task via RDP:

1.  Force task (if required)
2.  Task context menu (right-click) -> click "Locate <MACHINE\_NAME>"
3.  Machine context-menu -> Stop server
4.  Machine context-menu -> Show remote desktop
5.  Use admin account

## **Stopping a project**

По инфе от Крылова, застопленные проекты перезапускаются после рестарта фермы.

For more details see this [thread](https://teams.microsoft.com/l/message/19:7a8fe7395a2d47288c29cfc421df6cbf@thread.skype/1556096726332?tenantId=e4d60396-9352-4ae8-b84c-e69244584fa4&groupId=8c31b3e5-5870-46b1-92a7-180d13b282ed&parentMessageId=1556096726332&teamName=DevExtreme&channelName=General&createdTime=1556096726332).

## **Easy test the latest installation**

Быстрый способ поставить последнюю инсталляху для проверки: взять сервер с нашей фермы и выбрать нужный скрипт из предложенных.

For more details see these [thread1](https://teams.microsoft.com/l/message/19:7a8fe7395a2d47288c29cfc421df6cbf@thread.skype/1556196608598?tenantId=e4d60396-9352-4ae8-b84c-e69244584fa4&groupId=8c31b3e5-5870-46b1-92a7-180d13b282ed&parentMessageId=1556196608598&teamName=DevExtreme&channelName=General&createdTime=1556196608598), [thread2](https://teams.microsoft.com/l/message/19:7a8fe7395a2d47288c29cfc421df6cbf@thread.skype/1556191192795?tenantId=e4d60396-9352-4ae8-b84c-e69244584fa4&groupId=8c31b3e5-5870-46b1-92a7-180d13b282ed&parentMessageId=1556191192795&teamName=DevExtreme&channelName=General&createdTime=1556191192795)

## **Add a new CCtray script**

See this [guide](https://supportserver/res/cctray-scripts/)

## **Update portable browser**

You'll need **dxVCS**

1.  Download Chrome Portable (e.g. from [https://portableapps.com/apps/internet/google-chrome-portable-64](https://portableapps.com/apps/internet/google-chrome-portable-64))
2.  Rename browser's folder to \`chrome-portable\`
3.  Add it to the **7z** archive, the name of the archive must correspond to the following pattern: \`**chrome-portable-x64-VERSION**\`, e.g. "chrome-portable-x64-86.0.4240.183.7z"
4.  Add the archive to the dxVCS -> $/CCNetConfig/Tools/PortableBrowsers/
5.  Update CCTrayConfig -> $/CCNetConfig/Server/Config/devextreme-MAJOR\_VERSION-qunit.xml, e.g. devextreme-21.1-qunit.xml
6.  You should update \`ChromeVersion\` parameter, it should reflect the **x64-VERSION** part of the portable chrome acrhieve name, e.g. ChromeVersion="x64-88.0.4324.104"
7.  CCTray -> force the $configWatcher task (can take some time because it waits until each updating project task finishes)
8.  Copy changes for "devextreme-xx.x-qunit.xml" files of all actual releases and force the $configWatcher task

For firefox the steps will be similar, the differences will be in the name of the archive(firefox-portable-x64-VERSION) and in the parameter name (FirefoxVersion instead of ChromeVersion)

For NodeJS version see $/CCNetConfig/Server/Config/devextreme-MAJOR\_VERSION-qunit.xml: there is NodeJSVersion="14.15.0"

## **Removing CI pipelines for discontinued builds**

**We should remove pipelines one month after marking build as discontinued.**

1.  Open DXVCS
2.  Checkout (Ctrl+O) the following files
    1.  *$/CCNetConfig/Server/Config/config-entities.ent*
    2.  *$/CCNetConfig/Server/Config/devextreme-XX.Y.xml* (here and below: replace XX.Y or XX\_Y with the version you need to remove)
    3.  If you checked out another file by mistake, do not forget to undo-checkout it (Ctrl+U)
3.  Open (F4 or Shift+~) config-entities.ent in your favorite code editor and remove the following strings:
    1.  *&devextreme\_XX\_Y\_qunit;*   
    2.  *&devextreme\_XX\_Y\_testcafe;*
    3.  *<!ENTITY  devextreme\_XX\_Y\_qunit SYSTEM "file:devextreme-XX.Y-qunit.xml">*
    4.  *<!ENTITY  devextreme\_XX\_Y\_testcafe SYSTEM "file:devextreme-XX.Y-testcafe.xml">*
4.  Open the *devextreme-XX.Y.xml* and remove:
    1.  All the *<smart queue="Tests">* and their descendants
    2.  A node containing the "*DevExtreme Demos Publishing"* string
    3.  A node containing the "*SitePublishingUrlReplacer*" string
5.  Commit (Ctrl+I) the *config-entities.ent* and *devextreme-XX.Y.xml* files. Do not forget to add a simple but descriptive commit message!
6.  Clone the [https://github.com/DevExpress/testcafe-visual-testing](https://github.com/DevExpress/testcafe-visual-testing) repository:
    1.  Remove the strings that match the .\*XX.Y.\* pattern from the [screenshot-reporter/ScreenShotReporter/App\_Data/Projects.xml](https://github.com/DevExpress/testcafe-visual-testing/blob/master/screenshot-reporter/ScreenShotReporter/App_Data/Projects.xml) file
    2.  Fix formatting
    3.  Publish the ScreenShotReporter project (using the VisualStudio menu: Build\\Publish)
    4.  Commit your changes
7.  Open DXCCTray
    1.  Find the *$configWatcher* task, right-click on it, and click the "*Force Build*" menu item
    2.  Wait until config watcher completes execution
8.  Go back to DXVCS and remove (Del) the following files:
    1.  *$/CCNetConfig/Server/Config/devextreme-XX.Y-qunit.xml*
    2.  *$/CCNetConfig/Server/Config/devextreme-XX.Y-testcafe.xml*