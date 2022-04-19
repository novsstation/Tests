---
title: Modules Metadata Generation
description: 
published: true
date: 2022-04-18T11:52:16.209Z
tags: 
editor: markdown
dateCreated: 2022-04-18T11:52:13.764Z
---


The modules metadata generator walks through *.d.ts* files, collects exports that have the `@public` or `@docid` doc tags, and saves the collected data to the *modules-meta.json* file. This file contains public exports grouped by a module:

```JSON
{
  ...
  "animation/frame": {
    "cancelAnimationFrame": {},
    "requestAnimationFrame": {}
  },
  "animation/fx": {
    "animationConfig": {},
    "default": {}
  },
  ...
}
```