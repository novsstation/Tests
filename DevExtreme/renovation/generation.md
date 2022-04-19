---
title: generation
description: 
published: true
date: 2022-04-18T11:24:49.726Z
tags: 
editor: markdown
dateCreated: 2022-04-18T11:24:47.072Z
---

# Особенности генерации компонентов под платформы

|№ | Особенность            | jQuery | React  | Vue  | Angular |
|:-------------:|:-------------: |:---------------: | :-------------:| :-------------:| :-------------:|
|1 | 2-way prop change event | `onValueChanged: handler` |  `valueChange={handler}` | `@update:value= "handler"` |`(valueChange)= "this.handler($event)"` |
|2 | set prop to `undefined` | если prop принимает null, то undefined будте вести себя как null, если нет - фоллбек до default value | игнор | фоллбек до default value | получит undefined|

1. `undefined` can not be used as special value for `TwoWay` props.

   `null` value should be used instead.

2. Component's refs now contain component or object with API methods (for React). Compare with old wrappers:

   Wrapper

   ```typescript
   <Button ref={this.buttonRef} {...props} />;
   this.buttonRef.instance.focus();
   ```

   New native component

   ```typescript
   <Button ref={this.buttonRef} {...props} />;
   this.buttonRef.focus();
   ```

3. Many API methods are removed.

   Almost all common methods are considered redundant for native components - `begin/endUpdate`, `dispose`, `element`, `getInstance`, `instance`, `on/off`, `option`, `registerKeyHandler`, `repaint`, `reset`, `resetOption` etc.

   Only component specific API methods (e.g. `focus`) are/should be implemented in declarative component. Also `defaultOptions` static method is implemented.

4. Some common events are removed.

   Common events are also considered redundant. These include `onDisposing`, `onInitialized`, `onOptionChanged`.

   `onContentReady` is described [here](####oncontentready-moved-to-jquery-wrapper).

   Component specific events (e.g. `onClick`) are implemented.

5. Event argument only contains event specific data.

   That means that `component` and `element` properties are removed from event argument.

   With removed API methods this may lead to the following cases:

   Old approach

   ```typescript
   onClick(e) {
     const buttonText = e.component.option('text');
     notify(`The ${this.capitalize(buttonText)} button was clicked`);
   }
   ```

   New approach

   ```typescript
   onClick(e) {
     const buttonText = e.event.target.textContent;
     notify(`The ${this.capitalize(buttonText)} button was clicked`);
   }
   ```

6. Nested components of nested components includes parent name (React and Vue).

   According to the docs, if we use few levels of nested components, and some nested properties have equal names on different levels - components should have different names.

   For example, in the Grid we have the `headerFilter` nested property and the `headerFilter` property for nested `columns` property. These options have equal name but different components:

   ```jsx
   <Grid>
     <HeaderFilter />
     <Column>
       <ColumnHeaderFilter />
     </Column>
     <Column>
       <ColumnHeaderFilter />
     </Column>
   </Grid>
   ```

   (https://js.devexpress.com/Documentation/Guide/Widgets/DataGrid/Filtering_and_Searching/)

   But now, in the wrappers we collect all possible options from all nested properties with the same name. So, in demo we can see the next code (and it works):

   ```jsx
   <Grid>
     <HeaderFilter />
     <Column>
       <HeaderFilter />
     </Column>
     <Column>
       <HeaderFilter />
     </Column>
   </Grid>
   ```

   (https://js.devexpress.com/Demos/WidgetsGallery/Demo/DataGrid/Filtering/React/Light/)

   In new components we support only first example.

7. Angular templates API is changed

   New Angular components use native template syntax with ng-template directive

   old syntax

   ```html
   <dx-button *ngFor="let item of items" text="Click Me!" template="template1">
     <div *dxTemplate="let data of 'template1'">
       <div style="border: 1px solid blue;">
         {{ data.text + "!" }}
       </div>
     </div>
   </dx-button>
   -->
   ```

   new syntax

   ```html
   <dx-button
     *ngFor="let item of items"
     text="Click Me!"
     [template]="template1"
   >
     <ng-template #template1 let-data="data">
       <div style="border: 1px solid blue;">
         {{ data.text + "!" }}
       </div>
     </ng-template>
   </dx-button>
   -->
   ```
8. #### `onContentReady` moved to jquery wrapper

    `onContentReady` is implemented in jquery wrapper now. It raises after:
    
    - first render
    - `repaint` method call
    - option change if option is specified on `_getContentReadyOptions` method. If `beginUpdate/endUpdate` methods are used, the event raises once after `endUpdate` method.

    If you wanna extend options set which raise `contentReady`, you should override `_getContentReadyOptions` method in your widget this way:
    ```
    _getContentReadyOptions(): string[] {
      return [...super._getContentReadyOptions(), 'width', 'height'];
    }
    ```

    If you don't wanna raise an event by this rule, you should override `_fireContentReady` method as empty.

    If you need to pass `onContentReady` option value to declaration (it's very bad), you should get `restAttributes.onContentReady`.