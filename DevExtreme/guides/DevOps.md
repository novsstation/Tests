---
title: DevOps
description: 
published: true
date: 2022-04-21T11:09:55.424Z
tags: 
editor: markdown
dateCreated: 2022-04-18T12:14:30.249Z
---

## **Internal NPM Registry**

[http://npmproxy:4873/](http://npmproxy:4873/)

**Note**: VPN is required

Examples:

> npm i devextreme@21.2-next --registry [http://npmproxy:4873/](http://npmproxy:4873/)

> yarn add devextreme@21.2-next --registry [http://npmproxy:4873/](http://npmproxy:4873/)

`npx` doesn't support the `--registry` flag, you can use the corresponding environment variable (affects current process, e.g. terminal instance):

> set npm\_config\_registry=[http://npmproxy:4873/](http://npmproxy:4873/%20)  
> npx devextreme-cli -v

If you need a nightly build, you should specify the XX-next tag

## **Updating a Docker image**

[https://github.com/DevExpress/DevExtreme/tree/20\_2/build/docker-image](https://github.com/DevExpress/DevExtreme/tree/20_2/build/docker-image)

-   Нужно знать докер
-   Собирается образ, с чистого листа
-   Метится временным тегом\* и проверяется на отдельной ветке (или локально, если времени не жалко)
    -   `docker build -t devexpress/devextreme-build:YYYY-MM-DD`
-   Если всё норм, то помечается тегом XX\_X
    -   docker tag devexpress/devextreme-build:YYYY-MM-DD devexpress/devextreme-build:XX\_X docker push devexpress/devextreme-build:XX\_X

\* Этот вариант - с заливкой на девэкстримоский хаб, чтобы иметь возможность залить образ и манипулировать тегами - необходимо иметь соответствующие права на хабе

## **Gulp**

Don't use `path.join` within `gulp.src` since it incorrectly determines [glob base](https://gulpjs.com/docs/en/api/concepts#glob-base) (Possible WA: use `base` or `cwd` [option](https://gulpjs.com/docs/en/api/src#options))

See [https://github.com/gulpjs/gulp/issues/2085](https://github.com/gulpjs/gulp/issues/2085)

## **GitHub Actions**

### **Style Guide (YAML)**

**Naming conventions**

-   Workflow name is noun-like. It's a name for a group of assertions
-   Job name is noun-like. It's an assertion
-   Step name is verb-like. It answers a question "what to do?" (like a commit message)
-   When something fails a human see `<Workflow name> / <Job name>` on the GitHub. A couple of these names should make sense
-   Names are for humans. It means words separated by spaces, the first starts with a capital, no period in the end

Good:

A name for something

Bad:

a name for something A name for something. A-name-for-something A\_NAME\_FOR\_SOMETHING

**Letter Case**

All that can be used with dot notation is lowerCamelCased

-   secrets
-   step ids
-   script variables (bash)
-   jobs
-   environment variables (except for 3rd party variables)

Other YAML keys should be kebab-cased if possible

**Newlines**

YAML is sparse enough and there is no need for extra lines except for this cases:

-   before and after each job
-   before and after each step  
     

**Spaces**

-   2 spaces are used for tabulation
-   Array items are prefixed with tabulation and a '-' symbol

Good:

types:   - opened

Bad:

types: - opened

## **Useful Tips**

### **Use env variables**

For better readability use env variables for github context values:

\- name: Check version bump PRif:  steps.versionBump.outputs.changed  env:     title: ${​​​​​​​{​​​​​​​github.event.pull\_request.title}​​​​​​​​​​​​​​​​​​​​​​​​​​​​}​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​    version: ${​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​{​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​steps.versionBump.outputs.version}​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​}​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​

### **Multiline scripts**

YAML has several ways of breaking string over multiple lines (e.g. see [this article](https://www.baeldung.com/yaml-multi-line)). These are the most common for writing scripts:

-   Literal style (recommended)

Keeps line breaks but reduces empty lines at the end of the string

run: |   echo foo   echo bar

-   Folded style

Line breaks are replaced by space characters for consecutive non-empty lines

run: >  echo foo  echo bar

Joining lines into one can result in unexpected errors in bash, thus Literal style is recommended.

### **FAQ**

**Why checks frozen with "Expected - Waiting for status to be reported" status?**

This occurs when the check is marked as required in the branch protection rules, but was not triggered for the PR

More details: [https://github.community/t/expected-waiting-for-status-to-be-reported/18001](https://github.community/t/expected-waiting-for-status-to-be-reported/18001)

Why some checks disappear after changes were added to the branch?

It seems that GitHub only lists the checks from the latest check suite. If a check is not triggered on `synchronize` event it won't be included in the latest suite.

More details: [https://github.community/t/bug-report-failed-status-checks-getting-removed-after-commit-from-the-github-action-bot/17370](https://github.community/t/bug-report-failed-status-checks-getting-removed-after-commit-from-the-github-action-bot/17370)

## **hg**

**Наши репозитории:**

-   [https://hg/mobile](https://hg/mobile)
-   [https://hg/devextreme-metadata-tools/](https://hg/devextreme-metadata-tools/)
-   [https://hg/HgAdapter/](https://hg/HgAdapter/)

**Если завис адаптер:**

-   может залочиться репозиторий. Можно попробовать запустить `hg recover` (на машине hg в директории C:\\Hg\\repos\\mobile, по RDP туда есть доступ у Мартынова, Звягина, Митрохина, Жаворонкова)
-   See more -

[Alexey Martynov (DevExpress): Boris Krylov (DevExpress) сообщает: каккаято беда …](https://teams.microsoft.com/l/message/19:d6e62127a8034edebaa1d4c6050e3150@thread.skype/1586334136182?tenantId=e4d60396-9352-4ae8-b84c-e69244584fa4&groupId=f74b7d18-34a4-4c78-b7d5-b56e55ce3236&parentMessageId=1586334136182&teamName=Teams%20Collaborations&channelName=DevExtreme%20CI%20and%20DevOps&createdTime=1586334136182) 

posted in Teams Collaborations / DevExtreme CI and DevOps at Apr 8, 2020 11:22 AM

**Syncer bot:**

-   sources: [https://github.com/DevExpress/devextreme-repo-syncer/](https://github.com/DevExpress/devextreme-repo-syncer/)
-   Check bot state via ssh (*login: dx, password: dx, port: 22*):

> ssh dx@devextreme-mini-server
> 
> sudo -H bash  
> cd /opt/devextreme-repo-syncer/  
> ./tail.sh

To restart containers, follow the steps from the previous point, but instead of the *./tail.sh* run: *./stop.sh*, then *./start.sh*

**More info about hg adapter:**

HGAdapter is a middleware that enables Mercurial as VCS for CCNet. It allows to check for modifications, and to get changed files in the DXBuild-acceptable format.

You can find sources in the following repo: [_https://github.com/DevExpress/HgAdapter_](https://github.com/DevExpress/HgAdapter)

After changing, you should

1.  Build the solution in the **Release** configuration
2.  Publish the result to the DXVCS at: **$/CCNetConfig/Server/hg/**

If you need to change DXBuild-specific parts of code, you need to modify one (or both) of the following files (DXVCS links below):

-   $/InternalSoftware/DXBuild/DXBuild.Core/Mercurial.cs
-   $/InternalSoftware/DXBuild/DXBuild.Core/MercurialDriver.cs
-   When changing any of the files above, ask Boris Krylov directly to update DXBuild

To see HGAdapter logs, check out the following directory:

-   [_\\\\ciserver\\LocalProjects\\DevExtreme\\21.2\\QUnit\_Build_](https://teams.microsoft.com/_)
-   You can modify the directory above according to the task you need to analyze

**Виснущий докген**

*(Если hg recover не помогает)*

Иногда синхронизилка создаёт коммит, но убивается до того, как замёржит (по неясным причинам, возможно, таймаут таски). После этого HG говорит что-то типа "у тебя тут куча head-ов, выбери что-то или отстань от меня"  
Поэтому, локальные головы можно прибить, учитывая, что они особо не нужны:

-   при помощи hg outgoing можно посмотреть что мы будем лить на сервак *(login: buildmaker, password:buildmaker)*
-   если что-то есть, то:
    -   для начала надо разрешить экстеншен strip - для этого откроем файл hgrc в папке .hg, впишем следующее:

> \[extensions\]
> 
> strip =
> 
> либо не впишем, если уже вписано

-   При помощи данного экстеншена можно эти коммиты (и их наследники) прибить
-   Будем убивать по комиту, они идут от старых к новым (сверху вниз). Учтите, что наследники коммитов будут убиваться, иногда команда hg strip может ругнуться на несуществующий коммит.
-   После убивания коммитов мы придём к тому, что hg outgoing скажет, что локальных ченжей больше не осталось (мы всё вычистили).