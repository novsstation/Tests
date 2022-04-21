---
title: Documentation Generation
description: 
published: true
date: 2022-04-21T11:21:07.400Z
tags: 
editor: markdown
dateCreated: 2022-04-18T11:49:54.118Z
---

# Topics Generation

Use the [update-topics](Commands#update-topics) command to generate documentation. It requires the path to root folder of [documentation repository](https://github.com/devexpress/DevExtreme-documentation) and the *Declarations.json* file.

Topic generator generates an md file for each [member](Discovering#Members). A generated topic consists of the following three sections separated by `---`:

```MarkDown
---
id: dxAccordion.Options.height
type: Number | String | function()
default: undefined
---
---
##### shortDescription
Specifies the UI component's height.

##### return: Number | String
The UI component's height.

---
Here is the full description.
```

The first section contains single-line attributes

```MarkDown
---
id: dxAccordion.Options.height
type: Number | String | function()
default: undefined
---
```

, the second section - attributes that can have multiline value

```MarkDown
---
##### shortDescription
Specifies the UI component's height.

##### return: Number | String
The UI component's height.

---
```

, the third secion includes only the full description.

```MarkDown
Here is the full description
```

If documentation folder is empty, topic generator saves .md files with description stubs to the *NewDocs* subfolder. Then a techwriter can move these files to other folders according to the documentation structure and fill the descriptions. If the documentation is already structured, topic generator updates topics if needed keeping their paths. New topics that do not have parent are generated to *NewDocs* folder. Path to a new child topic is calculated depending on its parent's path.

All short descriptions and deprecation notes are saved to a dictionary where a key is a member id and serialized to *descriptions.json*.

```JSON
. . . ,
"dxValidationGroupResult": {
  "shortDescription": "A group validation result.",
  "depNote": "Use ValidationResult instead."
},
. . .
```

This file is used to inject descriptions to code (see [Descriptions Injection](#descriptions-injection)).

# Descriptions Injection

The **DevExtreme.Descriptions.Injector** replaces stubs in a specified file or multiple files with an appropriate description or deprecation note. Here is an example of stubs (*dx.all.d.ts*):

```TypeScript
/**
  * [descr:dxValidationGroupResult]
  * @deprecated [depNote:dxValidationGroupResult]
  */
export interface dxValidationGroupResult {
  . . .
}
```

