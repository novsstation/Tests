---
title: Metadata Generation
description: 
published: true
date: 2022-04-21T11:03:49.616Z
tags: 
editor: markdown
dateCreated: 2022-04-18T11:51:07.229Z
---

# Integration Metadata

Integration metadata is required to generate React and Vue wrapers for DevExtreme components. Integration meta is generated based on the *Declarations.json* and *modules-meta.json* files. Use any of the following commands to generate integration meta:

- [integration-data-generator](Commands#integration-data-generator) - Sequentially runs **ModulesMetaGenerator** and **IntegrationDataGenerator**. Requires *Declarations.json* file and the path to DevExtreme sources.
- [update-integration-meta](Commands#update-integration-meta) - Sequentially runs [discovering](Discovering) and then **ModulesMetaGenerator** and **IntegrationDataGenerator**. Requires only the path to DevExtreme sources.


Integration metadata is used in the [devextreme-react](https://github.com/DevExpress/devextreme-react) and [devextreme-vue](https://github.com/DevExpress/devextreme-vue) repositories.

# Angular Metadata

Angular metadata is required to generate Angular wrapers for DevExtreme components. You can generate Angular metadata using one of the following commands:

- [generate-ng-smd](Commands#generate-ng-smd) - Runs the **NgSmdGenerator**. Requires the *Declarations.json* file.
- [generate-smd-ng](Commands#generate-smd-ng) - Sequentially runs [discovering](Discovering) and then **NgSmdGenerator**. Requires the path to DevExtreme sources.

This metadata is used in the [devextreme-angular](https://github.com/DevExpress/devextreme-angular) repository.

# Strong Metadata

Strong metadata is required to generate ASP.NET MVC wrapers for DevExtreme components. Generate strong metadata using the [generate-smd](Commands#generate-smd) command, that runs the **SmdGenerator**. This command requires the *Declarations.json* file.
