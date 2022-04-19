---
title: Discovering
description: 
published: true
date: 2022-04-18T11:47:39.369Z
tags: 
editor: markdown
dateCreated: 2022-04-18T11:47:36.795Z
---

Discovering tools parse DevExtreme source files and generate metadata (*Desclarations.json* file) that provides full information on public declarations. This metadata is used as an input to generate integration metadata, strong metadata, and documentation.

Discovering includes two steps: [TypeScript discovering](#TypeScript Discovering) and [main discovering](#Main Discovering).

# TypeScript Discovering

**TypeScript Discoverer** collects raw declarations metadata from *d.ts* files and outputs it as *ts-members-meta.json*. This meta goes to the input of the main Discoverer.

Raw metadata includes two sections:

## Members

This section provides information on DevExtreme components, their methods and properties.

The declaration is considered as a member if it is:

* exported or is a property of exported type or interface,
* has the `@docid` or `@const` doctag.

```TypeScript
/**
 * @docid
 * @public
 */
export function cancelAnimationFrame(requestID: number): void;
```

```TypeScript
export interface dxButtonOptions extends WidgetOptions<dxButton> {
  /**
   * @docid
   * @public
   */
  activeStateEnabled?: boolean;
  . . .
}
```

```TypeScript
/**
* @const
*/
declare const devices: DevicesObject;
export default devices;
```

The information about member type is stored in *ts-members-mbeta.json* as a list of doc tags. 

```JSON
{
  "tags": {
    "docid": [
      "AnimationConfig.complete"
    ],
    "public": [
      ""
    ],
    "type": [
      "function($element, config)"
    ],
    "type_function_param1": [
      "$element:DxElement"
    ],
    "type_function_param2": [
      "config:any"
    ],
    "type_function_return": [
      "void"
    ]
  },
  . . .
},
```

In most cases these tags are generated automatically based on the member declaration. However, if the required tag value differs from the generated one, you can add the corresponding tag to the member's doc tags section in the code to override the generated value:

```TypeScript
/**
* @docid
* @type_function_param2 config:object
* @public
*/
complete?: (($element: DxElement, config: any) => void);
```

## Types

The **Types** section describes public types and interfaces that are marked with the `@public` doc tag but don't have the `@docid` or `@const` tags and all the types that they reference.

```TypeScript
/** @public */
export type CancelClickEvent = Cancelable & EventInfo<dxActionSheet>;
```

# Main Discovering

The Discoverer tool collects members information based on doc tags found in *.js* files, merges this information with the TS Discoverer's output, and serializes full members metadata to *Declarations.json*. The **types** section is copied from *ts-members-meta.json* to *Declarations.json* as is.

# Validation

**DevExtreme.Declarations.IntegrityValidator** validates DevExtreme public declarations. It accepts the `--js-scripts` argument that spcifies the path to DevExtreme sources.