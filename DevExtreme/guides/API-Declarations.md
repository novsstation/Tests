---
title: API Declarations
description: 
published: true
date: 2022-04-21T11:06:42.925Z
tags: 
editor: markdown
dateCreated: 2022-04-18T13:05:36.359Z
---

## **FAQ on how to work with declarations**

1.  Q: У нас появились новые d.ts файлы, разложенные почти везде. Зачем?

A: эти d.ts файлы - модули - у нас есть уже давно, но раньше они генерировались при билдежке и были плохими (слабая типизация, неправильные экспорты, падения в рантайме). Теперь они стали чуть лучше и - стали сорцами, а не генерируемым кодом, и теперь мы можем их использовать для улучшения нашего TS и МетаДанных

2) Q: док-тэги (док-комменты) есть и в .js и в .d.ts файлах. Какие-то из них не нужны?

A: Нужны и те и те. С первого раза не удалось автоматически перенести все док-тэги из .js в .d.ts, поэтому часть осталась на своих местах (чаще всего это поля вложенных объекты).

3) Q: Я пишу новую декларацию, что для этого нужно?

A: Нужно внести соотв. изменения в d.ts файл: добавить TS-декларацию и приклеить к нему док-тэг. В .js писать НОВЫЕ док-тэги в общем случае НЕ НУЖНО (в частном случае пишите сюда в канал)

4) Q: Я меняю старую декларацию, что для этого нужно?

A: Нужно внести соотв. изменения в d.ts файл: обновить TS-декларацию. Предполагается, что док-коммент уже есть (мы же меняем старую декларацию), если он в .d.ts - меняем в d.ts, если в .js - меняем в .js. Т.е. все просто - где лежит, там и меняем.

5) Q: нужно ли обновлять dx.all.d.ts ?

A: да, так же, как и раньше, см. [Updating dx.all.d.ts](https://teams.microsoft.com/l/entity/com.microsoft.teamspace.tab.wiki/tab::2bd851b6-bd63-41ab-bde1-8f1c9de4b600?context=%7B%22subEntityId%22%3A%22%7B%5C%22pageId%5C%22%3A28%2C%5C%22sectionId%5C%22%3A30%2C%5C%22origin%5C%22%3A2%7D%22%2C%22channelId%22%3A%2219%3A7a8fe7395a2d47288c29cfc421df6cbf%40thread.skype%22%7D&tenantId=e4d60396-9352-4ae8-b84c-e69244584fa4).

6) Q: Сложно-сложно-ничего-не-понятно, зачем так?

A: ~~Денег нет, но вы держитесь~~ Сорцы находятся в процессе миграции, в скором будущем вся мета-инфа будет только в d.ts, потом вместо док-тэгов информация будет браться напрямую из TS-декларации, а потом и вместо d.ts+.js будут только .ts. Будет гибче, стабильнее, и удобнее (-:

## **Useful Tips**

1.  в .d.ts файлах док-тэги достаются только из типов, которые экспортятся (прямо или косвенно, как тип какого-то поля). Просто повесить блок док-тэгов "в воздухе", не привязанных ни к какому мемебру не выйдет. В .js так можно.
2.  в .d.ts файлах нельзя писать больше одного блока док-тэгов для одного элемента. Один многострочный коммент - это ОК. Несколько многострочных или однострочных - не ОК.
3.  для указания имени в .js файлах используется тэг @name, в .d.ts - @docid

## **Internal purposes warning**

`**Warning! This type is used for internal purposes. Do not import it directly.**`

Это сообщение, которым у нас помечаются **все не публичные TS типы**.

После билдежки пакета специальная тулза пробегает по сорцам и ко всему, что может заимпортить пользователь и что не помечено тэгом `@public` приклеивает это сообщение. Так должно помечаться всё, что непублично, если что-то где-то не пометилось, или, наоборот, пометилось зря - пишите в тред: [Warning! This type is used for internal purposes. Do no…](https://teams.microsoft.com/l/message/19:7a8fe7395a2d47288c29cfc421df6cbf@thread.skype/1595940663832?tenantId=e4d60396-9352-4ae8-b84c-e69244584fa4&groupId=8c31b3e5-5870-46b1-92a7-180d13b282ed&parentMessageId=1595940663832&teamName=DevExtreme&channelName=General&createdTime=1595940663832) 

## **Updating dx.all.d.ts**

1.  d.ts генерируется на основе доккоментов. Для того, чтобы скорректировать существующие опции\\методы или добавить новые - надо обновить доккоменты.
2.  Для генерации d.ts - запустить **npm run update-ts**

## **Updating StrongMetaData.json**

StrongMetaData.json is stored in the hg/mobile repo and is used for generating ASP.NET (and Core) wrappers.

Once the API declarations are changed the corresponding DevExtreme StrongMetaData Check task will generate a new StrongMetaData.json.

If changes detected the task goes red

To update the StrongMetaData.json in the repository go to the \\DevExtreme.AspNet.Mvc folder and run the Update-Mvc-Metadata.ps1 script:

> powershell.exe -executionpolicy unrestricted ./Update-Mvc-Metadata.ps1

After that you can check the updated version grabbed to your local repository, commit it and push. The task will go green after that.

## **Hiding inherited properties**

Assuming we need to add a new type `DerivedType` derived some, but not all the properties from `BaseType`.

Step 1 provides clean public type for TS projects.

Steps 2 and 3 make doc topics work properly.

[Playground](https://www.typescriptlang.org/play?ssl=28&ssc=2&pln=21&pc=1#code/PTAEF5K6fAoEoAKAnApugjgVwJYGdcAXNfBMWSqOGxAeQFtjQATAe1NADs2jQ0AHgT64uoACoBlUAB5QAZgB0AVkUBGADSgA7mlAALAIYA3PUTahs+PW21j9aADYAHDKCIBPV+VC4GzthQ+SQBrXGdQADMUNgZQAHIAK3xgAGNAtGBRFkF4gG44QQCg9y89UPCZcS0AaX4BEi4WfFAQtA82SIkAPghkXFSQqq0AUQFUx2wcmTaOrurQGu7ugp92VIBaIkMAcxbDdFB8MOdXFl8xIgd6w39HNALREhRIw1S9ACFDa3Ey0ABvOCgYE5FC4UwsVBsZwALm42AYACMMAVgQZcCwclwACIYcFoSExWFHIhgrg7AoAX1oFColB8Y1uznuPjp9NoACoOQACgACzmwiMcA25HOAhQExSI3M8rm5uLBEN+cvAoAqzhkCvxLGVaA+jkMXBCGm58X0GKxWohUOc8V6ADIAXBuS7ucAuc7XaK+QKhQNPa6ebz1hiAy6xUC0bYuDaYdz8KTRBS4NSEB7vfzBcLUs6gyHzlaCbrc3yioE+IWdWVc+KnhhXu9QJXdfrDSFuYJGs1uV8fn9-oBoAiHw6HYfdHLDGfNmLQXEnebYqQx8rxSrKimnltXBJt8-FrvRM5x28J0Ljho8VJHI6AA)

### **Step 1**

Add a public type skipping hidden properties. Note it is a `type`, not an `interface`. `DerivedTypeBlank` is defined in the next step.

Add new properties if required. The properties must have `docid` without value (it is calculated automatically)

```plaintext
/** @public */
export type DerivedType = Skip<DerivedTypeBlank, 'hiddenDerivedProp'> & {​​​
    /**
     * @public
     * @docid
     */
    ownProp: string;
}​​​​​​​​​​
```

### **Step 2**

Add an`interface` called  `DerivedTypeBlank`. This is an intermediate type for holding doc-tags.`Blank` is a common suffix used in such cases.

The blank type

-   is not for customers' usage and **must not be exported**
-   must have explicit `docid` tag with value
-   must have explicit `export` tag with value: the name of the **public type** defined in the previous step - `DerivedType` (not the blank type)
-   must have explicit `inherits` tag with value: docid of the base type  
     

### **Step 3**

Override inherited properties that should be removed.

The properties

-   must have explicit `docid` tag value: the name of the **public type** defined in the previous step - `DerivedType` (not the blank type) plus the property name.
-   should have `any` type.

```plaintext
 /**
 * @docid DerivedType
 * @export DerivedType
 * @inherits BaseType
 */
interface DerivedTypeBlank extends BaseType {​​​​​​​​​​​​​​​​​​
    /**
     * @hidden
     * @docid DerivedType.hiddenDerivedProp
     */
    hiddenDerivedProp: any;
}​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​
```