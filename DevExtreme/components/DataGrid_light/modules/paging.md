---
title: paging
description: 
published: true
date: 2022-04-21T10:58:11.184Z
tags: 
editor: markdown
dateCreated: 2022-04-18T11:24:10.794Z
---

# Paging
 
- dummy realization with `Array.slice()`

## Breaking changes

- `pageSize` type now is `number | 'all'` instead of `number`. Settings `0` to this prop will work fine, but, in case it is changed from pager, it will be `'all'` instead of `0`. 

## Options

- [x] paging
  - [x] pageIndex
  - [x] pageSize
  - [x] enabled (discuss removing of this feature 

## Methods

- [ ] pageCount()
- [ ] pageIndex()
- [ ] pageSize()
