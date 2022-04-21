---
title: DevExtreme CLI
description: 
published: true
date: 2022-04-21T11:09:12.602Z
tags: 
editor: markdown
dateCreated: 2022-04-18T13:14:02.802Z
---

## **Repository structure**

The [devextreme-cli](https://github.com/DevExpress/devextreme-cli) repository contains 2 projects located in **/packages** folder:

-   devextreme-cli
-   devextreme-schematics

We use [Lerna](https://github.com/lerna/lerna) for managing those packages.

## **Git Branches**

Our branching strategy is a simplified version of [GitFlow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow). The main difference is that it's not always necessary to create a release branch for publication.

There are two main branches: **master** and **dev**. The **master** branch stores the package stable versions. The **dev** branch is used for implementing new features.

## **Features**

Feature branches should use **dev** as their parent branch.

Pull requests with new features should target **dev** branch.

## **Bugs**

Branches with bug fixes should be based on **master**.

The complete fix should be merged into both **master** and **dev**.

New features are merged from **dev** to **master** branch when they are tested and ready for publishing.