---
title: Release guide
description: 
published: true
date: 2022-04-19T06:01:40.923Z
tags: 
editor: markdown
dateCreated: 2022-04-19T06:00:58.444Z
---

## 1. Update Dependencies (Manual or Merge Renovate PRs)

There is manual instruction (preferred to merge PRs instead):

- Install the ['npm-check-updates'](https://www.npmjs.com/package/npm-check-updates) package globally
  ```
  npm i -g npm-check-updates
  ```
- Run npm-check-updates via lerna forcing updates for all packages
  ```
  yarn update-deps
  ```
- Ensure everything still works fine
- Check changelogs of the packages updated, remove packages from the package.json files which are no longer required

Note: Some Renovate PRs may duplicate packages in `yarn.lock` file. You should fix it manually, reinstall duplicated package or use command `npx yarn-deduplicate --packages *PACKAGE_NAME* yarn.lock`

## 2. Prepare release
on Master branch
Execute the following script: `npm run publish:prepare`.

`Make sure that all BC added to the changelog`

### 2.1. Merge Release PR Created by the Script

The script from the previous step will prepare a branch that you have to merge. 

### 2.2. Add Release to GitHub

A release tag should be applied on the commit with merged changes (from the previous step). Copy-paste content of the previous release and replace version with the version from the previous step.

__Don't forget to check "This is a pre-release" checkbox.__

## 3. NPM Publishing

Execute the following script: `npm run publish:npm`.

_NPM credentials_:

Login: <your_account_with_enabled_2FA> 
Password: <your_password>
!!!Email: **js@devexpress.com**
Token: <your_token>

### GitHub credentials & Algolia (necessary for updating Demos)

[Passwords](https://devexpress.sharepoint.com/:w:/r/sites/devextreme/_layouts/15/Doc.aspx?sourcedoc=%7Bd9751230-0c61-4af1-b7e5-ec7b8e50213c%7D&action=edit&uid=%7BD9751230-0C61-4AF1-B7E5-EC7B8E50213C%7D&ListItemId=90&ListId=%7B05C50FF8-674B-4315-8E50-D7CB0BFAD356%7D&odsp=1&env=prod)

## 4. Site Publishing

Execute the following script: `npm run publish:site`.

## Manual Publishing Guide (OUTDATED)

https://devexpress.sharepoint.com/sites/devextreme/_layouts/15/WopiFrame.aspx?sourcedoc=%7BD52497C2-3CD4-43AD-8481-0664B6B54565%7D&file=DevExtreme%20Reactive%20Release.docx&action=default

## Updating Demos after NPM publishing (OUTDATED)

Snippets Update(*Update MUI version)

##### Grid
- https://codesandbox.io/s/7o46mkowx
- https://codesandbox.io/s/13qvz1qqzl
- https://codesandbox.io/s/rymyjlonpq
- https://codesandbox.io/s/zqlr2lmxz3

##### Vue Grid
- https://codesandbox.io/s/k2zml29n4v

##### Chart
- https://codesandbox.io/s/vqo8yw5om7
- https://codesandbox.io/s/5x17l61xyk

##### Scheduler
- https://codesandbox.io/s/0y4zvoxl8v