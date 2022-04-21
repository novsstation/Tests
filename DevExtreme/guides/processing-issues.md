---
title: Processing Issues
description: 
published: true
date: 2022-04-21T11:11:55.291Z
tags: 
editor: markdown
dateCreated: 2022-04-18T12:23:39.086Z
---

## **Basic principles**

**1\. Проверить проект пользователя на ошибки, неправильное использование технологии, виджетов и т.д.**

**2\. Если есть проблемы, не связанные с вопросом кастомера - процессить их отдельно.**

**3\. Проверить, является ли то, на что жалуется кастомер его проблемой.**

Например, если он жалуется, что event файрится лишний раз, а у него весь код использования виджета неправильный и этот ивент ему и не нужен (характерно для Реакта, например) - для пользователя важно подсказать, как поправить код, а не разбираться с ивентом

4\. Упрощать пользовательский пример, пока баг воспроизводится.

Удалять ненужные файлы\\модули\\код\\стили\\хэндлеры\\данные - всё. В итоге получится МИНИМАЛЬНЫЙ ПРИМЕР, который можно разместить в какой-то онлайн-песочнице.

## **Non-jQuey project (that uses integration with ng, react, vue, etc)**

**5\. Определить, есть ли проблема именно в интеграции.**

Например, создать АНАЛОГИЧНЫЙ пример на jQuery. Аналогичный - это значит, виджеты в нем имеют такую же конфигурацию, как и в проекте пользователя. В опции передаются одинаковые значения, хэндлеры ведут себя одинаково, логика работы приложений одинаковая и т.д.

**6\. Локализовать проблему в виджете и передать инфу в Integration.**

Интеграция ничего не делает с виджетом такого, чего бы пользователь не смог сделать без интеграции!

Если проблема возникла "внутри виджета" - скорее всего, интеграция с ним неправильно взаимодействует (опции, ивенты, актуальность DOM, например "на момент инициализации div пустой и имеет нулевую ширину" или "в опцию ХХХ пришел undefined, а должно было значение ХХХ"). Отписать в ноты, что именно приводит к багу и перевести на Integration.

## **TypeScript Issues**

**Check if really the question is related TypeScript**

-   вместо ошибок компиляции приаттачены рантайм ошибки (приложение не может падать в рантайме из-за проблем с типами, TypeScript исчезает после компиляции проэкта)
-   кастомер использует в рантайме приватное API. Т.е. ему не просто нужны какие-то приватные типы, а он еще и делает что-то не то, завязывает рантайм своего приложения на наши приватные модули. Например: [https://github.com/DevExpress/DevExtreme/issues/17885#issuecomment-975156739](https://github.com/DevExpress/DevExtreme/issues/17885#issuecomment-975156739)  
    кастомер типы для приватных компонетов Scrollable, Overlay, DropDownEditor - лучше решать не вопрос "какие публичные типы порекомендовать кастомеру" а "что ему посоветовать, чтобы он не использовал приватные компоненты"

**Correctly determine the layer**

TypesScript problems can belong to several layers: devextreme package and wrappers packages.

We should first check if the problem occurs due to .d.ts file in the wrappers package (with help of the **Platforms squad**). If you get sure the problem is connected with the main package, then: if it is related to a particular component - contact the **Responsible squad**, if it is related to common types, or the whole type-system  - **Architecture squad**.

**Watch full error stack**

We need to have full error stack, one-line errors that customers send usually don't give enough information.

Compilation errors most often have several levels, but people only focus on the first level, especially if the stack is rather high.

E.g. in the [T1053548](https://supportcenter.devexpress.com/internal/ticket/details/T1053548) the customer send only this:

```plaintext
Type '(string | Column<any, any>)[]' is not assignable to type '(string | dxDataGridColumn<any, any>)[]'.
```

But the full error was:

```plaintext
Type '(string | Column<any, any>)[]' is not assignable to type '(string | dxDataGridColumn<any, any>)[]'.
  Type 'string | Column<any, any>' is not assignable to type 'string | dxDataGridColumn<any, any>'.
    Type 'Column<any, any>' is not assignable to type 'string | dxDataGridColumn<any, any>'.
      Type 'import("XXX/node_modules/devextreme/ui/data_grid").dxDataGridColumn<any, any>' is not assignable to type 'import("XXX/node_modules/devextreme/bundles/dx.all").default.ui.dxDataGridColumn<any, any>'.
        Types of property 'buttons' are incompatible.
          Type '("cancel" | "delete" | "edit" | "save" | "undelete" | import("XXX/node_modules/devextreme/ui/data_grid").ColumnButton<any, any>)[] | undefined' is not assignable to type '("cancel" | "delete" | "edit" | "save" | "undelete" | import("XXX/node_modules/devextreme/bundles/dx.all").default.ui.dxDataGrid.ColumnButton<any, any>)[] | undefined'.
            Type '("cancel" | "delete" | "edit" | "save" | "undelete" | import("XXX/node_modules/devextreme/ui/data_grid").ColumnButton<any, any>)[]' is not assignable to type '("cancel" | "delete" | "edit" | "save" | "undelete" | import("XXX/node_modules/devextreme/bundles/dx.all").default.ui.dxDataGrid.ColumnButton<any, any>)[]'.
              Type '"cancel" | "delete" | "edit" | "save" | "undelete" | import("XXX/node_modules/devextreme/ui/data_grid").ColumnButton<any, any>' is not assignable to type '"cancel" | "delete" | "edit" | "save" | "undelete" | import("XXX/node_modules/devextreme/bundles/dx.all").default.ui.dxDataGrid.ColumnButton<any, any>'.
                Type 'ColumnButton<any, any>' is not assignable to type '"cancel" | "delete" | "edit" | "save" | "undelete" | ColumnButton<any, any>'.
                  Type 'dxDataGridColumnButton<any, any>' is not assignable to type 'ColumnButton<any, any>'.
                    Types of property 'onClick' are incompatible.
                      Type '((e: import("XXX/node_modules/devextreme/ui/data_grid").ColumnButtonClickEvent<any, any>) => void) | undefined' is not assignable to type '((e: import("XXX/node_modules/devextreme/bundles/dx.all").default.ui.dxDataGrid.ColumnButtonClickEvent<any, any>) => void) | undefined'.
                        Type '(e: import("XXX/node_modules/devextreme/ui/data_grid").ColumnButtonClickEvent<any, any>) => void' is not assignable to type '(e: import("XXX/node_modules/devextreme/bundles/dx.all").default.ui.dxDataGrid.ColumnButtonClickEvent<any, any>) => void'.
                          Types of parameters 'e' and 'e' are incompatible.
                            Type 'import("XXX/node_modules/devextreme/bundles/dx.all").default.ui.dxDataGrid.ColumnButtonClickEvent<any, any>' is not assignable to type 'import("XXX/node_modules/devextreme/ui/data_grid").ColumnButtonClickEvent<any, any>'.
                              Type 'ColumnButtonClickEvent<any, any>' is not assignable to type 'NativeEventInfo<dxDataGrid<any, any>, PointerEvent | MouseEvent>'.
                                The types of 'component.addColumn' are incompatible between these types.
                                  Type '(columnOptions: string | import("XXX/node_modules/devextreme/bundles/dx.all").default.ui.dxDataGrid.Column<any, any>) => void' is not assignable to type '(columnOptions: string | import("XXX/node_modules/devextreme/ui/data_grid").Column<any, any>) => void'.
                                    Types of parameters 'columnOptions' and 'columnOptions' are incompatible.
                                      Type 'string | import("XXX/node_modules/devextreme/ui/data_grid").Column<any, any>' is not assignable to type 'string | import("XXX/node_modules/devextreme/bundles/dx.all").default.ui.dxDataGrid.Column<any, any>'.
                                        Type 'Column<any, any>' is not assignable to type 'string | Column<any, any>'.ts(2322)
```

## **Internal Types Requests**

У нас есть специальный ишью на ГитХабе: [Internal Types (#17885)](https://github.com/DevExpress/DevExtreme/issues/17885). Он нужен для того, чтобы мы могли собирать информацию о том, какие приватные типы используются в кастомерских проектах и либо опубличивать их, либо предлагать замену.

Тип считается приватным, если после сборки пакета у него есть такой тэг:

@deprecated Attention! This type is for internal purposes only. If you used it previously, please describe your scenario in the following GitHub Issue, and we will suggest a public alternative: {​​​​​​@link https://github.com/DevExpress/DevExtreme/issues/17885|Internal Types}​​​​​​.

Алгоритм обработки запросов примерно такой:

**Кастомер использует приватное API**

**A1**  ответить, что это неправильно, и что мы не гарантируем стабильную работу в этом случае.

Example:

Q: [17885#issuecomment-975156739](https://github.com/DevExpress/DevExtreme/issues/17885#issuecomment-975156739)

> We have a custom global extension to the JQuery object to provide DevExtreme callbacks. These seem to not have corresponding definitions.  
> interface JQuery {​​​​​​​​​​​​​​​​​  
>     dxScrollable(options: "instance"): DevExpress.ui.dxScrollable;  
>     dxScrollable(options: DevExpress.ui.dxScrollableOptions): JQuery;  
> ...​

A: [17885#issuecomment-977873202](https://github.com/DevExpress/DevExtreme/issues/17885#issuecomment-977873202)

> @Sixish, we do not recommend using these components at runtime because they are not public and are subject to change.  
> You can submit a ticket to our [Support Center](https://www.devexpress.com/ask) and describe your usage scenarios in detail. We'll see if we can recommend a public API for your tasks.

**Кастомеру нужен приватны базовый тип компонента**

(GridBase, BaseWidget, Overlay, etc.)

Если это простой случай, когда приватный тип используется для обработки нескольких компонетов (например, GridBase для хэндлера, использующегося и в dxDataGrid и в dxTreeList), то

**A2** ответить "используйте union"

Example:

Q: [17885#issuecomment-936398071](https://github.com/DevExpress/DevExtreme/issues/17885#issuecomment-936398071)

> what can I use instead of the following import?  
>   
> import {​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​ Component }​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​ from 'devextreme/core/component';

A: [17885#issuecomment-937532201](https://github.com/DevExpress/DevExtreme/issues/17885#issuecomment-937532201)

> If you need a type that matches different components, try defining a union: dxAccordion | dxActionSheet | ...

Если случай более сложный, то:

**A3** попросить примеры использования. нужно понять, как подобрать ему замену из публичных типов.

Example:

Q: [17885#issuecomment-904538685](https://github.com/DevExpress/DevExtreme/issues/17885#issuecomment-904538685)

> Can you tell us, what we can use instead of the following imports?
> 
> import {​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​ Component }​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​ from 'devextreme/core/component';  
> import {​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​ dxElement }​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​ from 'devextreme/core/element';  
> import DOMComponent from 'devextreme/core/dom\_component';  
> ...

A: [17885#issuecomment-904601987](https://github.com/DevExpress/DevExtreme/issues/17885#issuecomment-904601987)

> Could you give us usage examples for the Component, DOMComponent, and dxElement types?           

**Кастомеру нужен тип, который, кажется, должен быть публичным**

  
Нужно проверить, не был ли этот тип уже опубличен, скачав последний пакет. У публичных типов нет описанного выше тэга @deprecated. Также можно поискать тип в этой карточке [https://trello.com/c/jxzPk8cu](https://trello.com/c/jxzPk8cu) в списках с апдейтами в минорах

Если тип уже опбуличен, то

**A4** ответить "используй последнюю версию" и указать публичные типы, которые нужно использовать вместо приватных  
Example:

Q: [17885#issuecomment-984506813](https://github.com/DevExpress/DevExtreme/issues/17885#issuecomment-984506813)

> I am trying to import the following types:  
> import {​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​ dxFormButtonItem, dxFormEmptyItem, dxFormGroupItem, dxFormSimpleItem, dxFormTabbedItem, }​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​ from 'devextreme/ui/form';
> 
> Are there any alternatives to these types?

A: [17885#issuecomment-984557399](https://github.com/DevExpress/DevExtreme/issues/17885#issuecomment-984557399)

> @mfuatnuroglu, as for v21.1.6/v21.2.3, you can use these types instead:  
>   
> import {​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​ ButtonItem, EmptyItem, GroupItem, SimpleItem, TabbedItem, }​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​ from 'devextreme/ui/form';

Если нет, то нужно добавить тип в список Remained в [https://trello.com/c/jxzPk8cu](https://trello.com/c/jxzPk8cu) и

**A5** ответить "спасибо, добавили в очередь типов на ревью"  
Example:

Q: [17885#issuecomment-953631512](https://github.com/DevExpress/DevExtreme/issues/17885#issuecomment-953631512)

> I'm using the following 3 types which are declared as deprecated:
> 
> import {​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​ basePointObject, baseSeriesObject }​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​ from 'devextreme/viz/chart';  
> import {​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​ VizRange }​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​ from 'devextreme/viz/common';

A: [17885#issuecomment-954485286](https://github.com/DevExpress/DevExtreme/issues/17885#issuecomment-954485286)

> @Rondomat, thank you, I added these types to the review list.

Если тип уже был в списке Remained, то  
**A6** ответить "спасибо, это уже есть в списке, работаем над этим"  
Example:

Q: [17885#issuecomment-984506813](https://github.com/DevExpress/DevExtreme/issues/17885#issuecomment-984506813)

> I am trying to import the following types:  
> CustomRule like import {​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​ CustomRule }​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​ from "devextreme/ui/validation\_rules"

A: [17885#issuecomment-984557399](https://github.com/DevExpress/DevExtreme/issues/17885#issuecomment-984557399)

> CustomRule is already on the list, thanks.​​​​​​​

В остальных случаях подход к обработке - вопрос индивидуальный.  
 

Часто готовое сообщение содержит несколько типов ответов сразу, например в [17885#issuecomment-904601987](https://github.com/DevExpress/DevExtreme/issues/17885#issuecomment-904601987) есть **A4**, **A5**, **A3**.

## **Wrappers Related Issues**

Issues related to wrappers generation are assigned to Platforms Squad. If the problem is connected with incorrect metadata we should locate the wrong part of the corresponding .json file and forward the issue to the Architecture Squad.

## **A template to close issues on GitHub**

Thank you for the feedback/idea/comment/reply. We will think about it when planning to implement new features. Currently, we cannot provide you with an ETA on this. If we decide to work on this, we will post an announcement on GitHub, blogs, and Roadmap.

Change it depending on the situation and don't forget to check the text via correctors.