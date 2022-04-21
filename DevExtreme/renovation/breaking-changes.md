---
title: breaking changes
description: 
published: true
date: 2022-04-21T11:16:57.467Z
tags: 
editor: markdown
dateCreated: 2022-04-18T11:24:42.662Z
---

# Breaking Changes

## 21.1

- Use 'all' value for allowedPageSizes to add 'All' item into page size section of pager. We add default localization for it (dxPager-pageSizesAllText). (T725186, T535399)

- For controll of pager UI apperance use displayMode option in pager section. It can take on the following values: 'adaptive', 'compact' or 'full'. (T672366, T709640, T745052)

## 21.2

### Renovated component's markup should be changed through API (Button, Checkbox, all renovated widgets in the future)

Так как мы используем `virtual DOM`, любые изменения внутренней разметки пользователем из вне могут буть отменены при манипуляции с компонентом.
Для надежности все манипуляции с `DOM` компонента необходимо производить через его `API`. Это не относится к корневому элементу на котором создается виджет.
Потенциально, проблемы могут возникyть с методом `repaint()`, который ранее работал иначе.

### Assigning `undefined` to option resets it to default value or `null` (all widgets)

   To overcome Preact limitaion on setting `undefined` to TwoWay props, we changed the way jQuery widget process `undefined` option value.

   When user sets `undefined` to some option, jQuery widget pass option's default value or `null` if it is allowed by declaration.

   This does not affect option reading.

   ```ts
   $(selector).dxWidget("option", "someOption", undefined); // sets default value to someOption, e.g. 15

   $(selector).dxWidget("option", "someOption") === undefined; // true, jQuery widget stores user's values
   ```

   Current widgets implementation behaves pretty similar, so this change should be unnoticeable for users.
   

## Internal

1. ***EventsMixin***

    Убран *EventsMixin* и его наследование компонентами. Ранее он служил прослойкой, которая работала с *EventsStrategy*. Теперь это происходит внутри компонентов (*EventsStrategy* отрефакторен, методы *on* и *off* из миксина перенесены в компоненты).

    Док комменты показывают наследование методов *on* и *off* от *EventsStrategy*, но по факту *EventsStrategy* - поле (*_eventsStrategy*) компонентов (наследования как такового нет).

2. ***Сomponent._options***

    Теперь представляет собой экземпляр класса *Options*. Заменил собой *OptionManager* (избавились от дублирования полей), содержит все публичные методы, которые были у *OptionManager*. Обращение к полю напрямую с целью изменения опций крайне не рекомендуется, для этого в *Component* существуют специальные методы:

    * *option(option, value)* - получение/применение опции;
    * *_setOptionWithoutOptionChange(name, value)* - установка опции без триггера option changed;
    * *_getOptionValue(name, context)* - получение опции и привязка к context;
    * Установка опций без проверок *depricated* и *option changed* происходит через: *this._options.silent(option, value)*.

3. ***Сomponent._optionManager***

    Убран из *Component*, его роль выполняет *_options*. Класс *OptionManager* перемещен и используется внутри *Component._options* для хранения и работы с *options*.

4. *Diagram* имеет опцию *.export* и метод *export()* – в реновационных компонентах нельзя будет иметь одинаковые имена опций и методов

