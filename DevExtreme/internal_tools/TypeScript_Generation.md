---
title: TypeScript Generation
description: 
published: true
date: 2022-04-18T11:54:19.134Z
tags: 
editor: markdown
dateCreated: 2022-04-18T11:54:00.402Z
---

# Bundler Tool

`Bundler` is a tool that bundles all `*.d.ts` files into a single `bundle` file. A `bundle` is a file with a set of module declarations (namespaces).

```typescript
declare global {}

declare module DevExpress {}

declare module DevExpress.module1 {}
```

The bundling process starts with collecting all `public` types (types, interfaces, classes, etc.). A type is considered `public` if it is:

- exported and has the `@docid`, `@public`, or `@const` jsDoc tag.
- referenced by another `public` type.

```typescript

export interface NonPublicType { }

/** @docid */
export interface PublicType {
   field: AnotherPublicType;
}

export interface AnotherPublicType {}

```

The next step is to decide what namespace the `public` type belongs to.

There are two options:

- the namespace is set explicitly with the help of the `@namespace` jsDoc tag.
- the namespace is calculated based on the type file location and structure.

In the latter case, there are 3 options:

- if the type is declared in the `global` namespace, it is preserved in this namespace.
- the calculated namespace is a `DevExpress` string followed by the first folder name in `cwd`. E.g., for types in the `{cwd}/core/utils/math/calculation.utils.d.ts` file, the namespace is `DevExpress.core`.
- if there is the default export of some class in the file, this class is considered a widget class, and then the `public` type is placed in the nested module with the name of the exported widget class. E.g., for types in the `{cwd}/ui/data_grid.d.ts` file with the `dxDataGrid` class as the default export, the module is `dxDataGrid` inside the `DevExpress.ui` namespace.

In the last step, all jsDoc comments are transformed by the [Collapser](#collapser-tool).

For example, consider the following files:

```typescript
// {cwd}/ui/some_widget.d.ts

import { MyType } from '../core/utils';

export type SimplePropType = number;

/**
 * @public
 * @namespace DevExpress.ui.options
 */
export interface WidgetOptions {
    myProp?: MyType;
}

/** @public */
export default class Widget {
    getOptions(): WidgetOptions;
    getSingleProp(): SimplePropType;
}
```

```typescript
// {cwd}/core/utils.d.ts

export type MyType = string;

export type MyType = string;

export type MySuperType = any;
```

The result of bundling these files:

```typescript
declare module DevExpress.core {
    /**
     * @deprecated Attention! This type is for internal purposes only...
     */
    export type MyType = string;
}

declare module DevExpress.ui {
    module Widget {
        /**
         * @deprecated Attention! This type is for internal purposes only...
         */
        export type SimplePropType = number;
    }

    /**
     * [descr:Widget]
     */
    export class Widget {
        getOptions(): DevExpress.ui.options.WidgetOptions;

        getSingleProp(): DevExpress.ui.Widget.SimplePropType;
    }
}

declare module DevExpress.ui.options {
    /**
     * [descr:WidgetOptions]
     */
    export interface WidgetOptions {
        myProp?: DevExpress.core.MyType;
    }
}
```

To replace placeholders with actual descriptions or deprecation messages, use the [inject-descriptions-to-bundle](Commands#inject-descriptions-to-bundle) command.

# Collapser Tool

The collapser is an internal process that runs against `*.d.ts` files and simplifies jsDoc comments to prepare them for further usage. It is used by the [inject-descriptions](Commands#inject-descriptions) command as a first step and by [update-ts-bundle](Commands#update-ts-bundle) as a last step.

The collapser changes jsDoc comments following the rules below:

- the `@docid` or `@const` jsDoc tag is replaced with a placeholder for description.
- the `@deprecated` tag with a custom (or empty) message is preserved.
- the `@deprecated` tag with a reference to other types either by `docid` or `{file/path.typeName}` is preserved, but the reference is replaced with a placeholder for a correct deprecation message.
- all other tags or content of a jsDoc comment will be removed.
- if the original type has no `@public` tag or jsDoc comments, an additional `@deprecated` tag is added with a standard warning message stating that this type is for internal use.

Once the collapser process is completed, all jsDoc comments will contain only placeholders and meaningful deprecation messages.

Let's look at an example. Below is the initial file.

```typescript
/**
 * @docid
 * @public
 */
export interface WidgetProps {}

/**
 * @docid
 * @public
 * @deprecated WidgetProps
 */
export interface WidgetOptions {}

/**
 * @deprecated This is custom message
 * @public
 */
export type DeprecatedType = {};

/**
 * @docid
 * @public
 * @deprecated {file_path/file_name.TypeName}
 */
export type OldType = {};

export type InternalType = {};
```

And this is the result of the applied collapser:

```typescript
/**
 * [descr:WidgetProps]
 */
export interface WidgetProps {}

/**
 * [descr:WidgetOptions]
 * @deprecated [depNote:WidgetProps]
 */
export interface WidgetOptions {}

/**
 * @deprecated This is custom message
 */
export type DeprecatedType = {};

/**
 * [descr:OldType]
 * @deprecated [depNote.OldType]
 */
export type OldType = {};

/**
 * @deprecated Attention! This type is for internal purposes only...
 */
export type InternalType = {};
```